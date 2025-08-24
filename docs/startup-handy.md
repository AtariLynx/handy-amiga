# Configuring Epyx Handy development kit startup

Once the Epyx Handy development kit files have been restored from the 6 disk Quarterback backup set, the development environment needs additional changes to make it work correctly. 

The exact changes depend on the chosen setup:

- **Controllers without RDB support**  
  This scenario requires a bootable Old File System partition `BootPart` that mounts a second partition `AmigaHD` with Fast File System from the `devs/MountList` file.
  Example controllers are Commodore A2090 and A2090a. 
- **Controllers with RDB support**  
  Single partition `AmigaHD` with loadable Fast File System included in the `LSEG` parts. The controller used is the Commodore A590.

In all scenarios the main files are located on the partition called `AmigaHD`. These files should have been restored from the backup set earlier.

## Startup sequence

The most relevant files during booting and startup are located in both of the two partitions. A single partition setup will only use the files in `DH0B` (named `AmigaHD`). The two partition startup is only used for older disk controllers. 

**Boot partition:**

- `S/startup-sequence` startup script
- `FastFileSystem` file with the handler for the fast file system used for the `DH0B` partition
- `devs/MountList` with the definitions of the various devices, including `DH0B`

**AmigaHD partition:**

- `devs/MountList`, the same mount list file that is also be present on the main partition
- `S/Startup-Sequence.epyx`, with the rest of the startup that is run after the boot partition startup has finished
- `S/startup-sequence` startup script (if not booting directly from this partition)

## Two partition startup

The first partition is called `DH0` and named during format as `BootPart` or `BootPartition`. Its purpose is to mount the second partition `DH0B` named `AmigaHD`. Older controllers like the Commodore A2090 and A2090a also need a special `RES:` partition that is hidden and required for the initial setup of the drive. 

There are a couple of steps remaining to finish the setup of the Handy development kit. 

The startup script `S/Startup-Sequence` in the boot partition `BootPart` will mount the second partition `DH0B` (with logical name `AmigaHD`). 

```
c:cd c:
SetPatch >NIL: ;patch system functions
Sys:System/FastMemFirst ; move C00000 memory to last in list
Mount vdk:
BindDrivers

IF EXISTS DH0:c 
 ; hard disk is present
 dh0:c/cd     dh0:c             ; look for remaining commands on hard disk
 assign devs: dh0:devs          ; get remaining drivers, etc. from hd
 Mount  DH0B:                   ; mount FFS partition
 assign SYS:   DH0B:             ; switch everything over to it.
 assign c:     SYS:C
 assign L:     SYS:L
 assign S:     SYS:S
 assign DEVS:  SYS:Devs
 assign LIBS:  SYS:libs
 assign FONTS: SYS:Fonts
```

After mounting, it switches over all assignments of logical names to the newly mounted partition, as it contains the full Workbench installation.

If the `DH0B` partition is automatically mounted, the line with the `Mount DH0B:` statement must be commented out by adding a semi-colon at the front of the line.

```
; Mount  DH0B:                   ; mount FFS partition
```

In addition, the startup script needs some AmigaDOS commands like `if`, `else`, `endif` and for simple editing `ed`.

```
copy sys:system/format#? BootPart:system
copy c/ed BootPart:c
copy c/if BootPart:c
copy c/endif BootPart:c
copy c/else BootPart:c
```

![alt text](assets/workbench-copy-tools.png)

After you have copied over these files the setup is complete and you can boot into the new hardfile only configuration. Eject any `adf` files from the drive and restart the virtualized Amiga with `Ctrl+LeftAmiga+RightAmiga`. 

## Single partition startup

## Starting Handy development environment

Reboot the emulator and the Workbench screen should resemble this final result. The `BootPart` drive might not be present if you used a single partition drive.

![alt text](assets/handy-clean-startup.png)

In the `Handy Development Window` you can use the Handy tooling to build Atari Lynx software.

![alt text](assets/handy-asm.png)