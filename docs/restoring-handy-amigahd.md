# Restoring Epyx Handy development kit

This guide describes how to restore the *Quarterback* backup set with the Handy development kit. It is the 6 disk set that is available in this repository.

Required:

- WinUAE emulator
- Kickstart 1.3 ROM file (`amiga-os-130.rom`)
- Quarterback 4.3 or 5.0 disk file (as `adf` files)
- Workbench 1.3 bootable disk (`amiga-os-134-workbench.adf` or `a590-setup.adf`)

![alt text](assets/workbench-boot-quarterback.png)

Load the Amiga Kickstart 1.3 configuration you created earlier for your chosen setup. Make sure a Workbench 1.3 bootable floppy disk in inserted into drive `DF0`. You can use either the Workbench 1.3 Boot disk or the A590 Setup disk.

Start the emulator and verify that the AmigaHD drive is present. Insert the *Quarterback* floppy disk into drive `DF1`, open the `Quarterback` drawer and start the program.

![](assets/quarterback-drawer.png)

Depending on your setup the listed drives may differ. Select the main partition `AmigaHD` where the Epyx Handy files should be restored. Click on the `Restore` button for the next dialog.

In the next dialog keep `DF0` and `DF1` checked so two disk drives can be used to provide the backup set diskettes. Also, check `Restore empty drawers` to make sure empty folders are restored.

![alt text](assets/quarterback-amigahd-restore-options.png)

Click `OK` and insert disk `handy-16-disk1.adf` with the backup catalog in drive `DF0` when prompted.

![alt text](assets/quarterback-df0-not-backup.png)

After the list of files has loaded, click and tag the drawer `Empty` so it gets restored as well.

![alt text](assets/quarterback-amigahd-proceed.png)

> #### Need for an empty drawer
>  
> The `Empty` folder is needed to create new folders in Workbench 1.3. The older versions of Workbench did not have a way to directly create a new folder from a menu option. Instead, one would `Duplicate` the `Empty` drawer and `Rename` it afterwards. 

Click the `Proceed` button to go to the final dialog. Insert `handy-16-disk2.adf` into `DF1` and click on `Start` next.

![alt text](assets/quarterback-amigahd-restore-start.png)

During the restoring of the files you will be prompted to insert disks 3 to 6 at the appropriate time in the respective drives `DF0` and `DF1`.

The process should be finish almost as fast as you can swap disks. When it is done, close *Quarterback* return to Workbench. 
