# System Maintain Notes

- Install cuda locally

```bash
sudo ./cuda_9.0.176_384.81_linux-run --toolkitpath=/home/xueyan/cuda-9.0 --override #这么简单的东西吓了我一周
export PATH=/usr/local/cuda-9.0/bin:$PATH # input it in bashrc file, comment when don't need cuda9
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH
```


- Partition and mount a new disk

```bash
sudo rsync -av * /disk3/. # copy existing file
cat /proc/partitions # find the disk name to partition
sudo mkfs.ext4 /dev/xvdf # partition the disk
sudo mount /dev/xvdf /data/ # mount the disk
```

- Vitual Environment
```bash
pip install virtualenv # Installing virtualenv
virtualenv --version # Test your installation
cd py_env # go to the folder where you save virtual environment

virtualenv -p python3.5 virtualenv_name # create a virtualenv
or
python3 -m virtualenv -p python3 maskrcnn # sometimes virtualenv doesn't work

source virtualenv_name/bin/activate # start virtualenv
deactivate # exit virtualenv
```
