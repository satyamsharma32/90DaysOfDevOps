# Day 13 of learning linux volum-managment
# Day 13 – Linux Volume Management (LVM)

## Objective

Learn how to use Linux Volume Manager (LVM) to create, manage, extend, and mount storage volumes.

---

# Environment Setup

## Switch to Root User

```bash
sudo -i
```

or

```bash
sudo su
```

### Purpose

Administrative privileges are required for LVM operations.

---

# Create Virtual Disk (Optional)

If no spare disk is available:

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
```

### Purpose

Creates a 1GB virtual disk image.

---

```bash
losetup -fP /tmp/disk1.img
```

### Purpose

Attaches the disk image to a loop device.

---

```bash
losetup -a
```

### Purpose

Displays the assigned loop device.

Example:

```text
/dev/loop0
```

---

# Task 1: Check Current Storage

## Commands

```bash
lsblk
pvs
vgs
lvs
df -h
```

### Purpose

* `lsblk` → Shows block devices and partitions.
* `pvs` → Displays physical volumes.
* `vgs` → Displays volume groups.
* `lvs` → Displays logical volumes.
* `df -h` → Shows mounted filesystem usage.

### Observation

Reviewed current storage configuration before making changes.

---

# Task 2: Create Physical Volume

## Command

```bash
pvcreate /dev/sdb
```

or

```bash
pvcreate /dev/loop0
```

### Purpose

Initializes a disk for LVM usage.

---

## Verify

```bash
pvs
```

### Observation

New physical volume successfully created.

---

# Task 3: Create Volume Group

## Command

```bash
vgcreate devops-vg /dev/sdb
```

or

```bash
vgcreate devops-vg /dev/loop0
```

### Purpose

Creates a volume group named `devops-vg`.

---

## Verify

```bash
vgs
```

### Observation

Volume group created successfully.

---

# Task 4: Create Logical Volume

## Command

```bash
lvcreate -L 500M -n app-data devops-vg
```

### Purpose

Creates a 500MB logical volume named `app-data`.

---

## Verify

```bash
lvs
```

### Observation

Logical volume created successfully.

---

# Task 5: Format and Mount

## Format Logical Volume

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

### Purpose

Creates an ext4 filesystem.

---

## Create Mount Directory

```bash
mkdir -p /mnt/app-data
```

### Purpose

Creates a mount point.

---

## Mount Logical Volume

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

### Purpose

Makes the logical volume accessible through the filesystem.

---

## Verify Mount

```bash
df -h /mnt/app-data
```

### Observation

Logical volume successfully mounted.

---

# Task 6: Extend the Volume

## Extend Logical Volume

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

### Purpose

Adds 200MB to the existing logical volume.

---

## Resize Filesystem

```bash
resize2fs /dev/devops-vg/app-data
```

### Purpose

Expands the filesystem to use the additional space.

---

## Verify

```bash
df -h /mnt/app-data
```

### Observation

Filesystem size increased successfully.

---

# Verification Commands

```bash
pvs
vgs
lvs
lsblk
df -h
```

### Purpose

Verify the complete LVM setup.

---

# LVM Architecture

```text
Disk (/dev/sdb or /dev/loop0)
        │
        ▼
Physical Volume (PV)
        │
        ▼
Volume Group (VG)
        │
        ▼
Logical Volume (LV)
        │
        ▼
Filesystem (ext4)
        │
        ▼
Mount Point (/mnt/app-data)
```

---

# What I Learned

### 1. LVM Provides Flexible Storage Management

Logical volumes can be resized without repartitioning disks.

---

### 2. Storage is Managed in Layers

Physical Volume → Volume Group → Logical Volume.

---

### 3. Volumes Can Be Extended Easily

Additional storage can be added using `lvextend` and `resize2fs`.

---

# Commands Used

```bash
sudo -i
dd
losetup
lsblk
pvcreate
pvs
vgcreate
vgs
lvcreate
lvs
mkfs.ext4
mkdir
mount
df -h
lvextend
resize2fs
```

---

# Why This Matters for DevOps

LVM is widely used in production Linux servers because:

* Storage can be expanded without downtime.
* Application data volumes can grow as needed.
* Easier storage management in cloud and on-premise environments.
* Useful for databases, log storage, and application deployments.

---

# Screenshots

Add screenshots for:

* lsblk output
* pvs output
* vgs output
* lvs output
* Mounted filesystem
* Extended logical volume
* Final df -h output

