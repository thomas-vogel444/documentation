# Cheatsheet

Getting information:
- `du -h`: estimate file size in the current directory
- `df -h`: estimate disks size
- `fdisk -l`: lists the disks connected 
- `file -s <filename>`: type of file

Manipulating devices:
- `mkfs -t <filesystem> <diskname>`: initialises a filesystem on the disk selected
- `mount <devicename> <directory>`: mounts a device to a directory
