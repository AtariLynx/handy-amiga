# Configuring Epyx Handy development kit startup

Once the Epyx Handy development kit files have been restored from the 6 disk Quarterback backup set, the development environment needs additional changes to make it work correctly. 

The exact changes depend on the chosen setup:

- **Controllers without RDB support**  
  This scenario requires a bootable Old File System partition `BootPart` that mounts a second partition `AmigaHD` with Fast File System from the `devs/MountList` file.
  Example controllers are Commodore A2090 and A2090a.
- **Controllers with RDB support**  
  Single partition `AmigaHD` with loadable Fast File System included in the `LSEG` parts. The controller used is the Commodore A590.

In all scenarios the main files are located on the second partition called `AmigaHD`. These files should have been restored from the backup set earlier.

## Single partition startup

The  