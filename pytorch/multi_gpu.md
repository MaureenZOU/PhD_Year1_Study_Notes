# Multi-GPU

![alt text](https://github.com/MaureenZOU/PhD_Year1_Study_Notes/blob/master/pytorch/img1.png)

## Data parallel

```Python
device = torch.device("cuda:0") # This is the main device, it MUST be zero, and the sum data pool will be in this device.
model = nn.DataParallel(model)
model.to(device) 
mytensor = my_tensor.to(device) # 这三行指令顺序不是问题，主要是dataparallel要包住model
```


## Distributed

The package needs to be initialized using the ```Python torch.distributed.init_process_group()``` function before calling any other methods.


```Python
#!/usr/bin/env python
import os
import torch
import torch.distributed as dist
from torch.multiprocessing import Process

def run(rank, size):
    """ Distributed function to be implemented later. """
    pass

def init_processes(rank, size, fn, backend='tcp'):
    """ Initialize the distributed environment. """
    os.environ['MASTER_ADDR'] = '127.0.0.1' # These two, 'MASTER_ADDR' and 'MASTER_PORT' are the ports for multi-process jobs to communicate
    os.environ['MASTER_PORT'] = '29500'
    dist.init_process_group(backend, rank=rank, world_size=size) # The package needs to be initialized using the torch.distributed.init_process_group() function before calling any other methods
    fn(rank, size)

# It ensures that every process will be able to coordinate through a master, using the same ip address and port.

if __name__ == "__main__":
    size = 2
    processes = []
    for rank in range(size):
        p = Process(target=init_processes, args=(rank, size, run))
        p.start()
        processes.append(p)

    for p in processes:
        p.join()
```

## Maskrcnn Distributed
1. run distributed cmd line, master addr/port should be different for different process

```Python
python3 -m torch.distributed.launch --nproc_per_node=4 --master_addr 127.0.0.2 --master_port 29501 train_net.py
```

2. set local rank into arguement \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/55796a04ea770029a80cf5933cc5c3f3f6fa59cf/tools/train_net.py#L132)\]

```Python
parser.add_argument("--local_rank", type=int, default=0)
```
Because Torch distributed will automatically open multiple process, 1 and 2 link process with gpu rank, thus, each process could get its correct rank.

3. put cuda model to distributed class \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/55796a04ea770029a80cf5933cc5c3f3f6fa59cf/tools/train_net.py#L49)\]

```Python
if distributed:
    model = torch.nn.parallel.DistributedDataParallel(
            model, device_ids=[local_rank], output_device=local_rank,
            # this should be removed if we update BatchNorm stats
            broadcast_buffers=False,
            )
```

4. create distributed data sampler \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/master/maskrcnn_benchmark/data/samplers/distributed.py)\]

```Python
import math
import torch
import torch.distributed as dist
from torch.utils.data.sampler import Sampler


class DistributedSampler(Sampler):
    """Sampler that restricts data loading to a subset of the dataset.
    It is especially useful in conjunction with
    :class:`torch.nn.parallel.DistributedDataParallel`. In such case, each
    process can pass a DistributedSampler instance as a DataLoader sampler,
    and load a subset of the original dataset that is exclusive to it.
    .. note::
        Dataset is assumed to be of constant size.
    Arguments:
        dataset: Dataset used for sampling.
        num_replicas (optional): Number of processes participating in
            distributed training.
        rank (optional): Rank of the current process within num_replicas.
    """

    def __init__(self, dataset, num_replicas=None, rank=None, shuffle=True):
        if num_replicas is None:
            if not dist.is_available():
                raise RuntimeError("Requires distributed package to be available")
            num_replicas = dist.get_world_size()
        if rank is None:
            if not dist.is_available():
                raise RuntimeError("Requires distributed package to be available")
            rank = dist.get_rank()
        self.dataset = dataset
        self.num_replicas = num_replicas
        self.rank = rank
        self.epoch = 0
        self.num_samples = int(math.ceil(len(self.dataset) * 1.0 / self.num_replicas))
        self.total_size = self.num_samples * self.num_replicas
        self.shuffle = shuffle

    def __iter__(self):
        if self.shuffle:
            # deterministically shuffle based on epoch
            g = torch.Generator()
            g.manual_seed(self.epoch)
            indices = torch.randperm(len(self.dataset), generator=g).tolist()
        else:
            indices = torch.arange(len(self.dataset)).tolist()

        # add extra samples to make it evenly divisible
        indices += indices[: (self.total_size - len(indices))]
        assert len(indices) == self.total_size

        # subsample
        offset = self.num_samples * self.rank
        indices = indices[offset : offset + self.num_samples]
        assert len(indices) == self.num_samples

        return iter(indices)

    def __len__(self):
        return self.num_samples

    def set_epoch(self, epoch):
        self.epoch = epoch
```

5. communicate through process to get loss \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/55796a04ea770029a80cf5933cc5c3f3f6fa59cf/maskrcnn_benchmark/engine/trainer.py#L14)\]

```Python
def reduce_loss_dict(loss_dict):
    """
    Reduce the loss dictionary from all processes so that process with rank
    0 has the averaged results. Returns a dict with the same fields as
    loss_dict, after reduction.
    """
    world_size = get_world_size()
    if world_size < 2:
        return loss_dict
    with torch.no_grad():
        loss_names = []
        all_losses = []
        for k in sorted(loss_dict.keys()):
            loss_names.append(k)
            all_losses.append(loss_dict[k])
        all_losses = torch.stack(all_losses, dim=0)
        dist.reduce(all_losses, dst=0)
        if dist.get_rank() == 0:
            # only main process gets accumulated, so only divide by
            # world_size in this case
            all_losses /= world_size
        reduced_losses = {k: v for k, v in zip(loss_names, all_losses)}
    return reduced_losses
```

6. log in rank 0 \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/55796a04ea770029a80cf5933cc5c3f3f6fa59cf/maskrcnn_benchmark/utils/logger.py#L11)\]

```Python
if distributed_rank > 0:
        return logger
```

7. Util Funcs for distributed \[[link](https://github.com/facebookresearch/maskrcnn-benchmark/blob/master/maskrcnn_benchmark/utils/comm.py)\]


