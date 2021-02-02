---
title: quickly build a drive over a filesystem
published: true
date: 2021-01-28T23:05:10.410Z
tags: 
editor: undefined
dateCreated: 2021-01-28T23:05:10.410Z
---

i had some problems with a temporary filesystem (on memory) to speedup some cache work. 
the filesystem is shared (via vmware) on a windows machine and the filesystem is NTFS to easily use it under linux without too much constraints about (not so mature) tools (trying to build symlinks etc ...)
# building the loop drive in a file
````bash
nheim@nheim-virtual-machine:/mnt/shares/R$ mkfs -t ext4 ./ramdrive_over_ntfs 4500M
mke2fs 1.45.5 (07-Jan-2020)
Creating regular file ./ramdrive_over_ntfs
Creating filesystem with 1152000 4k blocks and 288000 inodes
Filesystem UUID: eccf9c38-db0b-47c7-a30b-2c3c9ecdc19e
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 

nheim@nheim-virtual-machine:/mnt/shares/R$ 
````

# mounting the loop file

````
nheim@nheim-virtual-machine:/mnt/shares/R$ sudo mount -t ext4 -o loop /mnt/shares/R/ramdrive_over_ntfs /mnt/cache/
````

# setting the yarn cache

````
yarn config set cache-folder /mnt/cache
````

# setting the npm cache

````
npm config set cache /mnt/cache/
````
# References 

- https://classic.yarnpkg.com/en/docs/cli/cache/

