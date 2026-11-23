# Linux LVM (Logical Volume Management) Lab Notes

## Objective
Create a Physical Volume (PV), Volume Group (VG), and Logical Volume (LV) using a newly added storage disk in RHEL. Format the LV with ext4 and mount it.

### Storage Configuration
- Disk: `/dev/vdb` (3 GB)
- Physical Volume: `/dev/vdb`
- Volume Group: `VGp`
- Logical Volume: `lv01`
- LV Size: 500 MB
- Filesystem: ext4
- Mount Point: `/mnt/lv01`

---

## 1. Verify Available Disks

List block devices and their mount points.

```bash
lsblk
```

Display disk and partition information.

```bash
sudo fdisk -l
```

Display filesystem information.

```bash
lsblk -f
```

---

## 2. Create Physical Volume (PV)

Initialize the new disk for LVM.

```bash
sudo pvcreate /dev/vdb
```

Verify Physical Volumes.

```bash
sudo pvs
```

Detailed PV information:

```bash
sudo pvdisplay
```

---

## 3. Create Volume Group (VG)

Create a Volume Group named `VGp` using `/dev/vdb`.

```bash
sudo vgcreate VGp /dev/vdb
```

Verify Volume Groups.

```bash
sudo vgs
```

Detailed VG information:

```bash
sudo vgdisplay VGp
```

---

## 4. Create Logical Volume (LV)

Create a 500 MB Logical Volume named `lv01` inside `VGp`.

```bash
sudo lvcreate -L 500M -n lv01 VGp
```

Verify Logical Volumes.

```bash
sudo lvs
```

Detailed LV information:

```bash
sudo lvdisplay /dev/VGp/lv01
```

---

## 5. Create Filesystem

Format the Logical Volume with an ext4 filesystem.

```bash
sudo mkfs.ext4 /dev/VGp/lv01
```

Verify filesystem type and UUID.

```bash
sudo blkid /dev/VGp/lv01
```

---

## 6. Create Mount Point

Create a directory where the filesystem will be mounted.

```bash
sudo mkdir -p /mnt/lv01
```

---

## 7. Mount Logical Volume

Mount the LV to `/mnt/lv01`.

```bash
sudo mount /dev/VGp/lv01 /mnt/lv01
```

Verify the mount.

```bash
df -hT
```

Check block devices and mount points.

```bash
lsblk
```

---

## 8. Test Storage

Create a test file.

```bash
sudo touch /mnt/lv01/test.txt
```

Write data to the file.

```bash
echo "Hello LVM" | sudo tee /mnt/lv01/test.txt
```

Read the file.

```bash
cat /mnt/lv01/test.txt
```

List files in the mounted filesystem.

```bash
ls -lh /mnt/lv01
```

---

## 9. Make Mount Permanent (Optional)

Get the filesystem UUID.

```bash
sudo blkid /dev/VGp/lv01
```

Edit the filesystem configuration file.

```bash
sudo vi /etc/fstab
```

Add the following entry, replacing the UUID with your actual UUID.

```text
UUID=89117655-fdb6-4d92-bfe4-82c7642e57c5 /mnt/lv01 ext4 defaults 0 2
```

Test the fstab configuration.

```bash
sudo umount /mnt/lv01
sudo mount -a
```

Verify the mount.

```bash
df -hT
```

## 10. Extend the Logical Volume
```
sudo lvextend -L +500M /dev/VGp/lv01
```

---

## 10. Essential LVM Commands Cheat Sheet

| Command | Description |
|---|---|
| `lsblk` | List block devices |
| `lsblk -f` | List disks, filesystems and UUIDs |
| `fdisk -l` | Display disk partition information |
| `pvcreate /dev/vdb` | Create a Physical Volume |
| `pvs` | Display Physical Volumes |
| `pvdisplay` | Detailed PV information |
| `vgcreate VGp /dev/vdb` | Create a Volume Group |
| `vgs` | Display Volume Groups |
| `vgdisplay VGp` | Detailed VG information |
| `lvcreate -L 500M -n lv01 VGp` | Create a 500 MB LV |
| `lvs` | Display Logical Volumes |
| `lvdisplay` | Detailed LV information |
| `mkfs.ext4 /dev/VGp/lv01` | Create ext4 filesystem |
| `blkid` | Display filesystem UUID and type |
| `mount` | Mount a filesystem |
| `umount` | Unmount a filesystem |
| `df -hT` | Display filesystem disk usage |
| `lvextend` | Extend a Logical Volume |
| `lvreduce` | Reduce a Logical Volume |
| `vgextend` | Extend a Volume Group |
| `vgremove` | Remove a Volume Group |
| `lvremove` | Remove a Logical Volume |
| `pvremove` | Remove PV metadata |

---

## 11. Final Storage Structure

```text
Disk: /dev/vdb (3 GB)
│
└── Physical Volume (PV)
    │
    └── Volume Group: VGp
        │
        └── Logical Volume: lv01 (500 MB)
            │
            └── Filesystem: ext4
                │
                └── Mount Point: /mnt/lv01
```

### Final Verification Commands

```bash
lsblk
sudo pvs
sudo vgs
sudo lvs
df -hT
```

### Important Notes
- PV is created using a disk or partition.
- VG combines storage from one or more PVs.
- LV allocates usable storage from a VG.
- A filesystem must be created before storing files.
- A filesystem must be mounted to access its contents.
- `/etc/fstab` is used for persistent mounts across reboots.
- Always verify the disk name before running `pvcreate` or formatting commands.
