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

## Mounting a Disk Partition

### Before mounting, make sure /dev/vdb1 has a filesystem:

- `sudo mkfs.ext4 /dev/vdb1`

#### Why Do We Need a File System?

A disk partition is like an empty piece of land. Before you can store and organize files on it, Linux needs a file system.

```
For example:

Disk
 └── Partition (/dev/vdb1)
       └── File System (ext4)
             ├── Files
             ├── Directories
             └── File Information
```
#### A file system tells the operating system:

- Where files are stored
- What blocks belong to each file
- File names and directories
- File permissions
- File ownership
- File size
- Free and used disk space

**Without a file system, Linux cannot properly organize normal files and directories on the partition.**

#### What Does mkfs.ext4 Mean?

```
The command:

sudo mkfs.ext4 /dev/vdb1

means:

mkfs = Make File System
ext4 = The type of file system
/dev/vdb1 = The partition where the file system will be created

It creates an EXT4 file system on /dev/vdb1.
```

#### What Happens to the Data?

⚠️ mkfs.ext4 destroys the existing filesystem structure and makes existing data inaccessible.

```
For example, imagine /dev/vdb1 contains:

/dev/vdb1
├── photo.jpg
├── document.pdf
└── project/

After running:

sudo mkfs.ext4 /dev/vdb1

The partition gets a new file system structure:

/dev/vdb1
└── EXT4 File System
    └── Empty Space

The old files are effectively lost/inaccessible and may be overwritten as the filesystem is used.
```

### Create Mount Point

- `sudo mkdir -p /mnt/disk1` - Mount in root directory
- `mkdir -p ~/mnt/disk1` - Mount in home directory

### Mount the Partition
- `sudo mount /dev/vdb1 /mnt/disk1`

### Verify
```
lsblk

or:

df -h

Expected:

vdb
└─vdb1   1G  part  /mnt/disk1
```

### To unmount the partition
- `sudo umount /dev/vdb1 /mnt/disk1`

### Persistent Mount
- First, identify the filesystem type - `lsblk -f`
- Create a mount directory - `sudo mkdir -p /mnt/disk1`
- Edit /etc/fstab - `nano /etc/fstab`
```
Format of /etc/fstab

UUID=<UUID>  <mount-point>  <filesystem-type>  <options>  <dump>  <fsck>

UUID=830ac5a0-e2ed-45d3-a4d8-ea5b11668dcb  /mnt/disk1  ext4  defaults  0  2
```
- Test the /etc/fstab entry - `sudo mount -a`

### Convert the partition to a Swap Space
- Format /dev/vdb2 as swap - `sudo mkswap /dev/vdb2`
- Enable the swap space. - `sudo swapon /dev/vdb2`
- To verify - `swapon --show`

## LVM (Logical Volume Manager)
LVM stands for Logical Volume Manager. It is a storage management system in Linux that provides more flexibility than traditional disk partitions.

```
Traditional partitioning
Disk → Partition → Filesystem → Mount

Example:

/dev/vda → /dev/vda3 → /
With LVM
Disk
 │
 └── Physical Volume (PV)
       │
       └── Volume Group (VG)
             │
             ├── Logical Volume (LV) → /
             └── Logical Volume (LV) → swap
```

### From your lsblk output:
```
vda3
├── rhel-root  → /
└── rhel-swap  → [SWAP]
```

### This means:

- /dev/vda3 is being used by LVM
- rhel is likely the Volume Group (VG)
- rhel-root is a Logical Volume (LV) mounted at /
- rhel-swap is a Logical Volume (LV) used as swap

### Why use LVM?
The biggest advantage is flexibility:

- ✅ Easily increase storage size
- ✅ Combine multiple disks into one Volume Group
- ✅ Create logical volumes
- ✅ Resize volumes (depending on filesystem/configuration)
- ✅ Create snapshots

### Useful LVM commands
```
# Show Physical Volumes
pvs

# Show Volume Groups
vgs

# Show Logical Volumes
lvs

# For detailed information:

pvdisplay
vgdisplay
lvdisplay
```
