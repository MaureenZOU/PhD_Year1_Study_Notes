# System Maintain Notes

- Partition and mount a new disk

```bash
sudo rsync -av * /disk3/. # copy existing file
cat /proc/partitions # find the disk name to partition
sudo mkfs.ext4 /dev/xvdf # partition the disk
sudo mount /dev/xvdf /data/ # mount the disk
```
