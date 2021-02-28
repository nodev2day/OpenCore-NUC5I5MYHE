# OpenCore-NUC5I5MYHE
Getting OpenCore working on Intel NUC5I5MYHE

## Hardware Details:

* Intel NUC5I5MYHE Intel Core i5-5300U 2.3 Ghz processor (Broadwell)
* Firmware upadted to the latest from the manufacturer (MYi50058 dated May 2020)

* 16 GB 1600 MHz DDR3 (2 Memory modules, slots full) Crucial CT102464BF160B.C16

* Storage 275 GB M.2-80 SSD boot (Crucial_CT275MX300SSD4) no optical drive


* Graphics Intel HD Graphics 5500 1536 MB

* Audio ALC283 

* Wired Intel I218LM3 PCI Express Gigabit Ethernet (IntelMausi)

* Wi-Fi 802.11ac Broadcom BCM43602 

* Bluetooth GMYLE Bluetooth 4.0 Broadcom Chipset 20702A3 Dongle Adapter USB



## Guides Used

* Dortania's OpenCore Install Guide 0.6.6 https://dortania.github.io/OpenCore-Install-Guide/
* Chris Titus YouTube video https://youtu.be/eUnVzJsINCI

## Prepare the Installer USB

Followed OpenCore 6.6 instructions with the DEBUG software download.  Use "Broadcom Laptop" instructions when in doubt.

I used Chris Titus YouTube video with Ventoy live Linux Mint distro to follow the guide and build the USB flash drive installer.  

Using Ventoy live Linux Mint distro on the target system you plan to install is much better than messing with Windows or even macOS tools/limitations.

Format a 4GB USB flash drive FAT32 using simple/first gdisk instructions in the guide - don't bother with a separate formatted EFI partition instructions.

Used gibMacOS to get Catalina recovery image (newest available from the catalog).

I did not make my own ACPI files like in the Chris Titus video and guide, I just grabbed the pre-compiled ones linked from the guide for Broadwell Laptop.

iMac16,1 is the SMBios I used for this model.

Do get your ethernet hardware address (from Bios) to fill into the config.plist.  The guide says its optional but I think the correct HW address was needed for ethernet to work.  

First time boot I got "DMG altered" and I went back to re-download Catalina recovery image with gibMacOS instructions, that resolved the problem.

From the EFI boot menu I chose "OPENCORE (external)" which was different than the guides, but makes sense as OPENCORE was the name of my USB installer drive.

With DEBUG file versions, it took 10 min to boot from USB drive each time.


## Kexts and Versions on USB Install Drive

* AppleALC-1.5.7-DEBUG.zip
* AirportItlwm_v1.2.0_stable_Catalina.kext.zip
* IntelBluetooth.zip
* IntelMausi-1.0.5-DEBUG.zip
* Lilu-1.5.1-DEBUG.zip
* VirtualSMC-1.2.0-DEBUG.zip
* WhateverGreen-1.4.7-DEBUG.zip

## ACPI Files on USB Install Drive

* SSDT-PLUG-DRTNIA.aml  (precompiled from the link in the guide under Broadwell Laptops)
* SSDT-EC-LAPTOP.aml (precompiled from the link in the guide under Broadwell Laptops)

## Result

After install, still booted from USB, everything worked: 

* audio yes
* wi-fi yes
* ethernet yes
* sleep yes  

With no on-board Bluetooth, I use a USB dongle (specs above) which works with is even working with handoff.

## Post Install Steps

Downloaded ProperTree and MountEFI to the SSD to make updates easily.

Followed relevant parts of Dortania OpenCore Post Install Guide to clean up
* Replaced DEBUG versions of OpenCore files with RELEASE versions on SSD EFI (per the guide)
* Changed macOS settings on SSD EFI to speed things up (no verbose, etc per the guide)
* Replaced DEBUG versions of all Kexts on the SSD EFI
* Wrote this readme :)


## Gotchas
### Booting from SSD, without installer USB

After successful first install from USB to SSD, I copied the EFI folder contents from USB to SSD.  

However, I still couldn't boot off the SSD - no bootable drives.

The trick was to mount the SSD's EFI partition and put both OC and BOOT folders in a new "EFI" folder.

So when mounted the path is like /Volumes/EFI/EFI/OC etc.

### gibMacOS Guide

gibMacOS ultimately worked bettery for me than macrecovery.py (current Dortania guide) for me to grab and unpack the Catalina restore image for booting USB.

However, I had a hard time finding a guide that included the long/complex uncompress "7s" command to split the .dmg and .chunklist from the .pkg file that gibMacOS downloads.

Here's the [diff of when the guide was changed](https://github.com/dortania/OpenCore-Install-Guide/commit/0e37df6c1690172a9e499d6c65dbca65b23b430a) and includes the gibMacOS instructions I used in the pink (deleted) text.
