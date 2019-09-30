# System Maintain Notes

- Install cuda driver

```bash
# (开心的第一次装了机器，有了自己的workstation :)
# install gcc and its accompanying tools
sudo apt-get install gcc
sudo apt-get install build-essential

# disable and stop gdm
sudo systemctl disable gdm
sudo systemctl stop gdm
sudo systemctl status gdm

# Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following contents
blacklist nouveau
options nouveau modeset=0
# Regenerate the kernel initramfs
sudo update-initramfs -u

# install
sudo ./cuda_9.0.176_384.81_linux-run --toolkitpath=/home/xueyan/cuda-9.0

# restart gdm
sudo systemctl enable gdm
sudo systemctl start gdm

```

- Install cuda locally
```bash
chmod +x cuda_9.0.176_384.81_linux-run
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

- Mount disk on linux automatically when boot
```bash
# ht小朋友教了各种实用tips ;)
sudo blkid # copy UUID
sudo vim /etc/fstab
UUID=ea65100b-c4b2-405d-a4f6-664f74563d8d /data         ext4    errors=remount-ro 0       1 # add this line to previous file
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
