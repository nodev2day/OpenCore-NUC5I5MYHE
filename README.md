# OpenCore-NUC5I5MYHE
Getting OpenCore working on Intel NUC5I5MYHE

## Hardware Details:

* Intel NUC5I5MYHE Intel Core i5-5300U 2.3 Ghz processor (Broadwell)

* 16 GB 1600 MHz DDR3 (2 Memory modules, slots full) Crucial CT102464BF160B.C16

* Graphics Intel HD Graphics 5500 1536 MB

* Audio onboard shows as Apple

* Wired Intel I218LM3 PCI Express Gigabit Ethernet en0

* Storage 275 GB SSD boot (Crucial_CT275MX300SSD4) no optical drive

## Prepare the Installer USB

Followed OpenCore 6.6 instructions with the DEBUG software download.

Used Chris Titus YouTube video with live Linux Mint distro to build the USB flash drive installer.

Format a 4GB USB flash drive MSDOS using gdisk - don't bother with a separate formatted EFI partition.

Used gibMacOS to get Catalina recovery image (newest available from the catalog).

iMac16,1 is the SMBios I used.

First time boot I got "DMG altered" and I went back to re-download Catalina recovery image, that resolved the problem.


## Kexts and Versions

* _Coming Soon_


## Post Install Steps

After install, still booted from USB, everything worked but BT (audio yes, wi-fi yes, ethernet yes, sleep yes).  

I have a USB BT dongle that works natively with previous Clover and also now with OpenCore.

Download ProperTree and MountEFI to the SSD so you can make updates easily.

## Gotchas
### Booting from SSD, without installer USB

After successful install, and copy EFI folder contents from USB to SSD, I still couldn't boot off the SSD - no bootable drives.

The catch was to mount the SSD's EFI partition and put both OC and BOOT folders in a new "EFI" folder.

So when mounted the path is like /Volumes/EFI/EFI/OC etc.
