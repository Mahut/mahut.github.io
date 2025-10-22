---
layout: post
title: Expanding a Proxmox VM Disk on Debian,
comments: true
tags: [guide, proxmox, debian, homelab]
---

> This post was generated largely by AI based on my notes.

## 1. Check the current layout

See how the disk and partitions are structured:

``` bash
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,TYPE
sudo fdisk -l /dev/sda
```

If you resized the disk in Proxmox, it shows a larger size for
`/dev/sda` but partitions still reflect the old size.

## 2. Fix the GPT table

`gdisk` corrects the GPT header so it matches the new disk size.

``` bash
sudo gdisk /dev/sda
```

Type `w` and confirm with `y`. This writes the corrected GPT to disk.

## 3. Reload partition table

Tell the kernel to reload the partition layout:

``` bash
sudo partx -u /dev/sda
```

If `partx` is missing, you can install `util-linux` or just reboot.

## 4. Expand the root partition

`growpart` automatically extends partition 1 to fill all remaining
space.

``` bash
sudo growpart /dev/sda 1
```

The output should confirm that partition 1 has grown.

## 5. Resize the filesystem

Extend the `ext4` filesystem to fill the new partition size:

``` bash
sudo resize2fs /dev/sda1
```

This can be done online while mounted.

## 6. Verify everything

Check the new size and ensure all space is available:

``` bash
df -h /
```

You should now see your full expanded disk space in use.

To confirm integrity:

``` bash
sudo gdisk -l /dev/sda && sudo e2fsck -n /dev/sda1
```

Both should report clean results.

The Debian root filesystem now uses the entire expanded Proxmox disk.
