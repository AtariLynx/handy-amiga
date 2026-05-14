# Hard disks for Handy development kit

The Handy development kit was introduced in a time where Commodore Amiga computers only had simple hard disks and early controllers. This was around the time of Kickstart and Workbench version 1.2. Later versions of the development kit were for version 1.3, but one can still find references to the early days of the Commodore Amiga and its hard disks

## Original hard disk configuration

The original documentation of the Handy development kit describes a Commodore Amiga 2000 or 500 with a 40 MB harddisk that has 2 partitions:

1. A boot partition `DH0` with the normal Old File System (OFS) named `BootPart` and a minimal set of startup files.
2. A second partition `DH0B` named `AmigaHD`, formatted with fast file system, to contain the Handy development kit files.

This is typical for the Commodore A2090 and Commodore A2090a hard disk controllers, which had special requirements to boot. The A2090 had no way to automatically boot and mount the hard disk. The later revision A2090a could mount a special `DH0` partition for an ST-506 XT drive, which included just enough to continue the boot process by mounting the second partition `DH0B`.

In the rest of the documentation you will find several approaches to the hard controller and disk configuration. This is to show alternative ways that the hard disk of the Amiga development machine can be set up.

## XT Hard disk types with ST-506 interface

There were a limited amount of hard disks available in 1988 to 1990 when the initial and later versions of the Handy development kits were released. Here is a list of ST-506 XT drives that work with a number of controllers mentioned below:

|Brand|Type|Surfaces|Sectors (per track)|Cylinders|Size (in MB)|
|---|---|---|---|---|---|
|Rodime|RO3055|6|17|870|40|
|Seagate|ST-138N|4|26|615|32|
|Seagate|ST-225|4|17|615|21|
|Seagate|ST-251|6|17|820|43|
|MiniScribe|8425|4|17|612|20|
|Toshiba|MK134FA|7|17|733|40|

These drives are using the Modified Frequency Modulation (MFM) data encoding method together with the ST-506 interface to connect the drive to the Amiga hard disk controller.

Later drives used IDE, ATA or SCSI and had both bigger capacity and more options.

## SCSI Hard disk types

One known type for the SCSI drives that were used by Commodore is as follows:

|Brand|Type|Surfaces|Sectors (per track)|Cylinders|Size (in MB)|
|---|---|---|---|---|---|
|Seagate|ST-325N|2|32|654|21|

## Hard disk controllers for Commodore Amiga

The hard disk controllers commonly used in the Commodore Amiga computers include the following:

|Controller|Boot partition|Main partition|Computer|
|---|---|---|---|
|Commodore A2090|DH0|DH0B|Amiga 2000|
|Commodore A2090a|DH0|DH0B|Amiga 2000|
|[Commodore A590](./a590-controller-setup.md)||DH0|Amiga 500|
|Commodore A2091||DH0|Amiga 2000|

The newer controllers A590 for the Commodore Amiga 500 and the A2091 card for the Amiga 2000 could boot and mount from a single partition, which is named `DH0` by convention. All controllers after the Commodore A2090 had Rigid Disk Block (RDB) support, allowing partition and file system information to be stored on the hard disk itself. 

The setup of the Handy development kit focuses on the controller type and uses one of the aforementioned hard disk types. You are free to select a different drive type that is compatible with a certain controller.