# Multi-GPU

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
