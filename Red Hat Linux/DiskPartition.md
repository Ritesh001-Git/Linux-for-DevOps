## Disk Partitioning Using fdisk

### 1. Check Available Disks
```
lsblk

Example output:

NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sr0            11:0    1 1024M  0 rom
vda           252:0    0   30G  0 disk
├─vda1        252:1    0  600M  0 part /boot/efi
├─vda2        252:2    0    2G  0 part /boot
└─vda3        252:3    0 27.4G  0 part
  ├─rhel-root 253:0    0 24.4G  0 lvm  /
  └─rhel-swap 253:1    0    3G  0 lvm  [SWAP]
vdb           252:16   0    2G  0 disk

The new disk is:

/dev/vdb
```

### 2. Open the Disk Using fdisk (Fixed/Format Disk)
```
sudo fdisk /dev/vdb
```

### 3. Create a New Partition

```
Inside the fdisk menu, type:

n

Select:

p

For the partition number, press:

Enter

For the first sector, press:

Enter

For the last sector, enter:

+1G
```

### 4. Check the Partition

```
Inside fdisk, type:

p

Example output:

Device     Boot Start     End Sectors Size Id Type
/dev/vdb1        2048 2099199 2097152   1G 83 Linux
```

### 5. Save the Partition
```
Type:

w

This writes the partition table to the disk.
```

### 6. Verify the Partition

```
lsblk

Expected output:

vdb           252:16   0    2G  0 disk
└─vdb1        252:17   0    1G  0 part
```
