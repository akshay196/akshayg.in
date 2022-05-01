---
title: Disk cloning using Clonezilla
date: 2022-03-19
tags: [tutorial, disk]
---

Yesterday, I was trying move Windows OS from the old disk to a new. At
first I thought of installing Windows on a new disk and then setup all
software that were already installed on old disk. But this seems
tedious and time consuming task, so while looking for other
alternatives, I come across know about
[Clonezilla](https://clonezilla.org/) tool.

Clonezilla is a FLOSS software for disk
[cloning](https://en.wikipedia.org/wiki/Disk_cloning) and
[imaging](https://en.wikipedia.org/wiki/Disk_image). It can save disk
images (i.e. backup disks), restore disk images and also clone
disk/partition to a new disk/partition. It is helpful tool for
replacing old, damaged disk with a new one.

Sine both of my disk are of a same size, I didn't require to shrink
the disk. The following procedure is to accomplish disk copying,
whether it could be your operating system or other disk with data:

1. It is recommended to backup your source disk.

2. All the data from target disk will be replaced with data from old
   disk. Hence an important data from target must be copied to
   somewhere else.

3. Boot Clonezilla live to USB drive. You can use
   [Tuxboot](https://tuxboot.org/) to create a bootable live USB
   drive.

4. Boot you machine with USB drive.

5. Select language and keyboard style.

6. Select disk to disk clone.

7. Select source disk and target disk properly.

8. Start cloning. This will take some time based on source disk data.

Once done, restart your machine. That's all you need. :D
