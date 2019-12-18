# Storage concepts

- Device names
    - /dev/fd0: first floppy drive
    - /dev/fd1: second floppy drive
    - /dev/sda: first hard disk detected
    - /dev/fsdb: second hard disk detected
    - /dev/xvda: first Xen Virtual Device
    - /dev/xvdb: second Xen Virtual Device
    - /dev/xvda1: first partition of the first Xen Virtual Device
- Filesystem
    - Linux: ext4, ext3
- Partition
    - Primary partition 
        - Logically independednt section of a hard disk
    - Extended partition
        - primary partition that has been divided up into logical partitions to create more than 4 partitions