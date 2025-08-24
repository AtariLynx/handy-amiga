# Handy development environment installation guide for WinUAE

This guide will help you prepare a virtualized setup of the Handy development environment using the Commodore Amiga emulator WinUAE. The aim is to replicate the environment as closely as possible, using the original setup of a Commodore Amiga 2000 or 500 and a harddisk.

The guide involves several steps and assumes you have some experience in using AmigaOS and Workbench.

The preparation steps are as follows:

1. Prepare a virtual hard disk with required partitions.
2. Create an emulator configuration for the Commodore Amiga 500/2000.
3. Mount, format and restore partitions of the prepared hard disk.
4. Finish setup, including startup sequence and additional preparation.
5. Create final WinUAE configuration

The final Handy development environment requires version 1.3 of both Kickstart and Workbench. If you plan to follow along with step 1 to 4, it will additionally require Kickstart and Workbench version 3.1. However, the resulting hard disk is included in the repository that contains the `adf` and `hdf` files for the Handy development environment. It allows you to skip step 1 to 4 and use the `hdf` file in the final step.
It is recommended to skip to step 5 and setup the WinUAE environment with the resulting hardfile. It saves a substantial amount of time.

> ### Acquiring Kickstart and Workbench versions
> 
> You can acquire the required Kickstart and Workbench files as part of an [Amiga Forever](https://www.amigaforever.com/) package. 
> 
> At the time of writing the Value edition only has support for the Amiga 500 with Kickstart 1.3 and Workbench 1.3. This is sufficient to setup the development environment. 
>
> However, should you want to manually configure the virtual hard disk for the environment, you will need the Amiga Forever Plus package (or Premium) that includes the newer versions (including 3.1).

### Prerequisites:

**Required:**

- WinUAE emulator
- Kickstart 1.3 ROM file (`amiga-os-130.rom`)

**Optional:**

- Workbench 1.3 Boot disk (`amiga-os-134-workbench.adf`)
- Kickstart 3.1 ROM files (`amiga-os-310-a1200.rom`)
- Workbench 3.1 Install disk (`amiga-os-310-install.adf`)
- Quarterback 4.3 or 5.0 disk file (as `adf` files)

The optional files are only needed if you want to create the hardfile in step 1 to 4. 

# Step 1 (optional): Creating a 2 partition disk with FastFileSystem

Use any Commodore Amiga configuration with Kickstart 3.1. Open the WinUAE properties dialog (by pressing `F12`) and go to `Settings > Hardware > CD & Hard drives` in the left tree structure.

Create a new hardfile at the bottom area of the dialog. Enter 40 MB as the size and click `Create`.
Save the hardfile as `epyx-handy-16.hdf`, to indicate its purpose for Epyx Handy development kit 1.6.

The newly created hardfile will automatically be selected at the top dropdown. Name the drive `DH0`. Make sure that the `Full drive/RDB mode` is not selected. Also, the configuration of this drive should be:

|||
|---|---|
|Surfaces|1|
|Sectors|32|
|Reserved|2|
|Block size|512|

![alt text](assets/winuae-create-hardfile.png)

 Insert the "AmigaOS 3.1 Install" floppy diskette into `DF0` (`amiga-os-310-install.adf`) and start the emulator. After the booting has completed, open the drawer `HDTools` and select the `HDToolBox` icon. Do not start it, but instead open the "Information" dialog by keeping the right mouse button pressed and going to the top menu in Workbench.

![alt text](assets/hdtoolbox-information.png)

Check the lines of the "Tool types" that read:

```
SCSI_DEVICE_NAME=scsi.device
SCSI_MAX_ADDRESS=6
SCSI_MAX_LUN=7
XT_NAME=  XT
```

![alt text](assets/hdtoolbox-edit-scsi.png)

Select the top line so it appears in the textbox next to the `New` and `Del` buttons. Change the line to use `uaehf.device` so the single line textbox becomes:

```
SCSI_DEVICE_NAME=uaehf.device
```

Make sure to press `Enter` before clicking on `Save`.

Start *HDToolBox* and find the new harddisk available as an SCSI interface with `Unknown` status.

![alt text](assets/hdtoolbox-startup.png)

Click on `Change Drive Type` and in the next dialog delete any existing drive types by selecting the drive type in the listbox and clicking on `Delete Old` until all have been deleted and the drive type listbox is empty. 

![alt text](assets/hdtoolbox-empty-drivetypes.png)

Next, click on `Define New...` to open a new dialog. 

![alt text](assets/hdtoolbox-new-drivetype.png)

Click the `Read Configuration` button. A message box appears to indicate that most information will be inferred from the drive. 

![alt text](assets/hdtoolbox-read-configuration.png)

Click `Continue` to read this information.

![alt text](assets/hdtoolbox-new-configuration.png)

Change the `Drive Name` to be `epyx` for your Epyx specific harddisk. Click the `Ok` button and in the next dialog `Ok` again.

![alt](hdtoolbox-drivetype-result.png)

You should now see that the other buttons also became available.

![alt text](assets/hdtoolbox-more-buttons.png)

Select the `epyx` drive and click the `Partition Drive` button.

The "Partitioning" dialog opens and shows existing partitions. 

![alt text](assets/hdtoolbox-default-partitions.png)

Delete any existing partitions. Click the left side of the disk layout drawing at the top and move the triangle shaped slider at the bottom of it to the left. The size of the first partition should be around 5 MB, sufficient for the few files that will be stored. Enter the `End Cyl` as `330` for the end cylinder.

![alt text](assets/hdtoolbox-first-partition.png)

Change the `Partition Device Name` to `DH0`, press `Enter`. Select the `Bootable` and `Advanced Options` checkboxes. The dialog will show additional options including button `Change...` and `Add/Update...` to configure the file system types. Click the `Change...` button.

![alt text](assets/hdtoolbox-dh0-filesystem.png)

In the "File System Characteristics" dialog edit the `MaxTransfer` value to be `0x0001fe00`. Uncheck the `Fast File System` and `International Mode` checkboxes. Click on `Ok` to return to the "Partitioning" dialog.

Create another partition by clicking the `New Partition` button. Click to the right of the first 5 MB `DH0` partition in the black rectangle indicating the remaining space on the disk.

![alt text](assets/hdtoolbox-second-partition.png)

Set the `Partition Device Name` to be `DH0B` and press `Enter` again. Make sure that the drive is not marked as `Bootable`, since it should not be booted from.

Go into "File System Characteristics" dialog by clicking `Change...`. Uncheck the `Auto-mounted this partition` to prevent automatic mounting of this partition as a drive. The startup script will take care of this later. 
Also, change the `MaxTransfer` value to be `0x1fe00` again. Click on `Ok` to save the changes in the current dialog.

![alt text](assets/hdtoolbox-dh0b-filesystem.png)

Back in the "Partitioning" dialog, click on the `Add/Update...` button. The "File System Management" dialog opens and it will probably show an existing `FastFileSytem` file system name of version 40.1 and identifier `0x444f5301`. This is not the correct file system, as the one included with the Handy development kit is of a different version.

Insert the "Handy Boot Disk" diskette `handy-16-boot.adf` into floppy drive `DF1`. Next, click on `Add New File System...` to add a different version of FastFileSystem.

![alt text](assets/hdtoolbox-enter-fastfilesystem.png)

The inserted Handy boot diskette is labeled `V1.3Boot`. You can provide the filename of the correct FastFileSystem as `V1.3Boot:l/FastFileSystem`. Click `Ok` and provide the version details of the FastFileSystem in the dialog that appears. It should be version `34` and revision `85`.

![alt text](assets/hdtoolbox-filesystem-details.png)

The DosType for the file system should be `0x444f5303`, which corresponds to the hexadecimal values for the characters `DOS3`. Click `Ok` to return to the "File System Maintenance" dialog that now shows an additional file system registered with a size of 12204 bytes. 

![alt text](assets/hdtoolbox-multiple-filesystems.png)

Delete the newer version `40.1` of the file system named `Fast File System`. Click `Ok` to return to the "Partitioning" dialog and close it by clicking `Ok` once more. Back in the "Hard Drive Preparation, Partitioning and Formatting" dialog you should see that the listed `epyx` harddrive now has a status of `Changed`. Commit the changes by clicking on the `Save Changes to Drive` button.

> ### Not enough space
>
> If you accidentally forgot to remove the `40.1` version of the file system, you will get an error indicating there is not enough room on the disk to save the changes.
>
> ![alt text](assets/hdtoolbox-space-warning1.png)
> ![alt text](assets/hdtoolbox-space-warning2.png)
>
> If so, retrace via `Partition Drive` and click `Add/Update...` to return to the "File System Maintenance" dialog and do remove the file system with version `40.1`.

![alt text](assets/hdtoolbox-single-filesystem.png)

Make sure the hard drive shows a status of `Not Changed`. Finish this part of the drive preparation by clicking the `Exit` button and return to Workbench.

At this point you can exit the emulator. Create a copy of the `epyx-handy-16.hdf` file to have a backup of the newly partitioned system.



## Step 3: Mount, format and restore partitions


Now that the mount list correctly defines the second partition `DH0B` it can be mounted and formatted.

```
assign Devs: BootPart:Devs
assign L: BootPart:L
mount DH0B:
format drive DH0B name AmigaHD FFS
```

After the formatting has completed, you should see a new drive called `AmigaHD` appear in Workbench.

## Step 3: Restore AmigaHD partition

Refer to the guide [Restoring Epyx Handy development kit](restoring-handy-amigahd.md) to restore the main files of the Epyx backup set.

## Step 4: Finalizing setup

