# Shrink exemple

````shell
root@slpreprdct01:~# resize2fs /dev/slpreprdct01-vg/home 1G
resize2fs 1.44.5 (15-Dec-2018)
Please run 'e2fsck -f /dev/slpreprdct01-vg/home' first.

root@slpreprdct01:~# e2fsck -f /dev/slpreprdct01-vg/home
e2fsck 1.44.5 (15-Dec-2018)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/slpreprdct01-vg/home: 16/331280 files (0.0% non-contiguous), 42366/1325056 blocks
root@slpreprdct01:~# resize2fs /dev/slpreprdct01-vg/home 1G
resize2fs 1.44.5 (15-Dec-2018)
Resizing the filesystem on /dev/slpreprdct01-vg/home to 262144 (4k) blocks.
The filesystem on /dev/slpreprdct01-vg/home is now 262144 (4k) blocks long.

root@slpreprdct01:~# 
root@slpreprdct01:~# lvreduce /dev/slpreprdct01-vg/home -L1G
  WARNING: Reducing active logical volume to 1,00 GiB.
  THIS MAY DESTROY YOUR DATA (filesystem etc.)
Do you really want to reduce slpreprdct01-vg/home? [y/n]: y
  Size of logical volume slpreprdct01-vg/home changed from 5,05 GiB (1294 extents) to 1,00 GiB (256 extents).
  Logical volume slpreprdct01-vg/home successfully resized.
root@slpreprdct01:~# 
````

# Extend exemple

````shell
root@slprdct01:~# lvremove /dev/slprdct01-vg/swap_1 ^C
root@slprdct01:~# vgextend slprdct01-vg /dev/sdb
  Physical volume "/dev/sdb" successfully created.
  Volume group "slprdct01-vg" successfully extended
root@slprdct01:~# lsblk
NAME                   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                      8:0    0   10G  0 disk 
├─sda1                   8:1    0  487M  0 part /boot
├─sda2                   8:2    0    1K  0 part 
└─sda5                   8:5    0  9,5G  0 part 
  ├─slprdct01--vg-root 254:0    0  2,2G  0 lvm  /
  ├─slprdct01--vg-var  254:2    0    1G  0 lvm  /var
  ├─slprdct01--vg-tmp  254:3    0  260M  0 lvm  /tmp
  └─slprdct01--vg-home 254:4    0  5,1G  0 lvm  /home
sdb                      8:16   0   20G  0 disk 
sr0                     11:0    1 1024M  0 rom  
root@slprdct01:~# 
````
