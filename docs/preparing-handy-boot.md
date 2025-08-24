# Restoring Handy boot partition

Run WinUAE and load the Handy configuration and add the hardfile of your choice. Make sure the Workbench 1.3 boot diskette is loaded into `DF0`. Start the emulator now.

Workbench 1.3 should open and show three drives on the desktop. 

![alt text](assets/workbench-drives.png)

One is called `DH0:` and in the two partition scenario it represents the first partition from which the Amiga will boot later. It needs to be formatted, or "initialized" as it is called under Workbench 1.3.

Select `DH0:` and right-click to select `Initialize` from the `Disk` top menu. There will be a few dialogs, which you should confirm to start the initialization. 

![alt text](assets/workbench-initialize1.png)
![alt text](assets/workbench-initialize2.png)

After a few seconds the name of the drive will change to `Empty`.

Assuring the drive is still selected, right-click to select `Rename` from the `Workbench` menu. Change the name to be `BootPart`.

> #### Format using a shell command
>  
> Alternatively, you can run a format command from the command-line in AmigaDOS Shell window:
>
> ```
> format drive DH0 name BootPart 
> ```
>  
> This might be useful for a installation script.

Now that the boot partition is formatted, the Handy backup for `DH0` (or `BootPart`) can be restored.

## Restoring boot partition backup

Insert the `quarterback-50.adf` diskette into `DF1` and open the drawer.

![alt text](assets/quarterback-drawer.png)

Start the *Quarterback* program. First, select the `BootPart` drive to restore to. After selecting that drive, click on `Restore`.

![alt text](assets/quarterback-dh0-restore.png)

On the next dialog with "Restore options" deselect drive `DF0` and select the option to `Restore empty drawers` and click `OK` to continue to the next dialog. 

![alt text](assets/quarterback-dh0-restore-options.png)

You will get a prompt that the inserted diskette is not a backup set. 

![alt text](assets/quarterback-backup-disk.png)

Insert `handy-16-dh0.adf` containing the backup set for the boot partition. It has just enough files to defer booting to the other partition `AmigaHD` which will be created later. Next, *Quarterback* will show all files in the backup set. 

![alt text](assets/quarterback-dh0-files.png)

Leave all files and folders checked, but do click on `T` and the `Tag` button to restore the empty `T` folder as well. Click on `Start` to restore the backup.

![alt text](assets/quarterback-start.png)

The restore progress will be reported and should complete quickly.

![alt text](assets/quarterback-dh0-restored.png)

Quit Quarterdeck and close the drawer as well. Eject the Quarterback backup disk `handy-hd0.adf` floppy from `DF1` as well. You can restart the emulator now if you want.

Open a new shell window by double clicking the Shell icon found in the `Workbench1.3` drive. Change the current folder to `BootPart:` using the CLI. Check the contents of the `l` folder.

``` 
cd BootPart:
dir l
```

You should see that the folder contains the following files:

```
Disk-Validator
FastFileSystem
Ram-Handler
vdk-handler
```

![alt text](assets/workbench-bootpart-handlers.png)

Similarly, ask for the directory contents of `devs`. Notice that there are two example `MountList` files available for the ST225 and ST251 Seagate drives originally used in the Amiga 2000 setup. 

```
cd devs
dir
```

Copy one of these files to a new file called `MountList`. This mount list file which will be used during mounting of devices. Start editing the file with the *Ed* editor found as `ed` under the `SYS:` assignment in the `c` folder.

```
copy MountList.ST225 MountList
SYS:c/ed MountList
```

![alt text](assets/workbench-copy-mountlist.png)

The *Ed* editor will open and show the contents of the `MountList` file. Scroll down to find an entry for the `VDK:` device using the `vdk-handler` from the `DH0:devs` folder.

```
VDK:	Handler = L:vdk-handler
		StackSize = 2000
		GlobVec = -1
		Priority = 5
#
```

Just above the `VDK:` entry you should also find the `DH0B:` entry. This is the device corresponding to the second partition of the hardfile, which has a partition with the same name `DH0B`. The entry needs to be changed based on the values of the second partition of the actual virtual drive created in step 1.

```
DH0B:
    Device = uaehf.device
    FileSystem = l:FastFileSystem
    Unit   = 0
    Flags  = 0
    Surfaces  = 1
    BlocksPerTrack = 32
    Reserved = 2
    Interleave = 0
    LowCyl = 331  ;  HighCyl = 2559
    Buffers = 30
    GlobVec = -1
    BufMemType = 1
    Mount = 1
    DosType = 0x444F5303
    StackSize = 2048
	MaxTransfer = 0x0001FE00
#
```

Save the modified contents of the `MountList` file by pressing the escape key `Esc` on your keyboard. An asterisk will appear at the bottom of the *Ed* program. type `x` and press `Enter` to save the file. You can use `q` and `Enter` to quit without saving after confirming with `Y`.

Next, a few missing commands need to be transfered to the boot partition for the `S/startup-sequence` script to work correctly. 


