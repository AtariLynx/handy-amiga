# Handy Software Development disks for Commodore Amiga

This repository contains Amiga diskettes in `adf` format for the Handy development environment, also known as "Lynx Development System". The `adf` files can be restored to physical 3.5" floppy disks to create a real-world setup of the environment on actual hardware.

In addition to the diskette files the repository also contains `hdf` hardfiles for use in the WinUAE emulator. It allows anyone to run an emulated Handy environment without the need for Amiga hardware. It is assumed that this scenario is most likely for those interested to work with Handy. 

**Currently only revision 1.6 (25th September 1991) is available.**

The virtualized Handy development environment requires the following:
- [WinUAE](https://www.winuae.net/download/) or [FS-UAE](https://fs-uae.net/download) emulator
- Kickstart ROM
- Workbench installation
- Quarterback backup software (optional)

Cloanto software offers [Amiga Forever](https://www.amigaforever.com/) software that provides various versions of Kickstart ROMs and Workbench hardfiles for nearly every Amiga system. It is a legal way to acquire the files needed to work with an emulated Amiga environment. Any Kickstart and Workbench version 1.3 or later will work. 

## Diskettes for Lynx Development System

The folder `adf` contains 8 diskette images in Amiga Disk File format.
- `handy-16-boot.adf`: Boot disk to use when booting from floppy disk instead of harddrive
- `handy-16-dh0.adf`: Quarterback 4.3 backup of boot partition `DH0`.
- `handy-16-disk*.adf`: Quarterback 4.3 backup set of Amiga development hard drive, consisting of 6 parts. 

The Handy boot disk can be used to boot directly from floppy disk on Amiga computers that do not have a hard drive.

Using the remaining disks requires the installation of the Quarterback program version 4.3 or 5.0. For your convenience the two backup sets have been restored into two hardfiles listed in the `hdf` folder: `handy-16-bootpart.hdf` and `handy-16-amigahd.hdf`.  

## Hardfiles with restored backups

The folder `hdf` contains several hardfiles for various purposes. 

The most important file is a accurately restored setup on a single hardfile with partitioning and file system as described in the original documentation.

- `handy-16-40mb-bootpart-amigahd.hdf`: 40 MB single hardfile with two partitions.

This hardfile can be mounted in a WinUAE configuration with Workbench 1.3. It contains two partitions:

1. A boot partition named `BootPart` with the normal Old File System (OFS) 
2. A second partition `AmigaHD` with the international fast file system to contain the Handy development kit files

In addition, there are two hardfiles for Amiga hard disks with the restored backups, without any modifications. These disk are not bootable. Instead, mount these disks as additional drives to access the contents if you do not have *Quarterback* software available.

- `handy-16-bootpart.hdf`: 1 MB hardfile with restored backup of set on `HandyDH0.adf` 
- `handy-16-amigahd.hdf`: 8 MB hardfile with restored backup of Lynx Development System on set of disks `handy-16-disk1.adf` to `handy-16-disk6.adf`.


