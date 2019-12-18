# Setting up EBS storage on a EC2 instance

From https://www.2daygeek.com/formatting-partitioning-and-mounting-drives-on-linux/

Assuming you have an EC2 instance with a EBS volume attached, you need to mount the volume to the filesystem of the host system. The EBS volume shows up as `/ect/xvdc`.

Note: `xvd` stands for Xen Virtual block Device

## Mounting the volume

Steps:
- Checking
    - `lsblk`: list the disks attached to the instance
    - `ls -la /dev/xvd*`: list the disks attached to the instance
    - `fdisk -l`: check the new hard drive size
    - `file -s /dev/xvdc`: checks that the volume is empty
- Create the partition
    - `fdisk /dev`: create the partition and press
        -> c: DOS compatibility flag not set
        -> u: Changing display/entry units to sectors
        -> n: adds a new partition
        -> p: set it as primary partition
        -> 1: set the partition number to 1
        -> w: write partition to disk 
- Create the filesystem on the disk partition
    - `mkfs -t ext4 /dev/xvdc`: format the volume with the ext4 filesystem
- Mount the partition's filesystem to the host's
    - `mkdir newvolume`: creates a new volume directory to mount the volume to
    - add `/dev/xvdc /newvolume ext4 defaults 0 0` to `etc/fstab`
        -> By default every reboot of the EBS volume will unmount any volume outside of the root volume.
    - `mount /dev/xvdc newvolume`: mounts the device onto the volume
- Final checks
    - `df -h`: check the amount of space on the new volume
    - `reboot`: reboots the server