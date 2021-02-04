# BASE-EFI

## Introduction
The Base EFI folder contains a prebuilt EFI that should be valid for all ASUS X299 motherboards.  It is currently built using OpenCore 0.6.6 with the OpenCanary GUI enabled following the Dortania OpenCore Vanilla Guide.

## 1. Important BIOS Settings
* Above 4G Encoding: Enabled
* MSR Lock: Disabled
* CSM: Disabled

## 2. Configuration
1. Ethernet: 
    * For WS X299 Sage/10G users replace IntelMausi with [SmallTreeIntel8259x](https://small-tree.com/support/downloads/10-gigabit-ethernet-driver-download-page/) kext and update the kext entry.  NOTE: Requires Ubuntu EEPROM modding outlined in @KGPs [guide section E.8.2.2](https://www.tonymacx86.com/threads/how-to-build-your-own-imac-pro-successful-build-extended-guide.229353/)
    * For users with I211 NICs like the X299 Deluxe, copy the [SmallTreeIntel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases) kext to your EFI folder and add a new kext entry under `Kernel-Add`
2. PlatformInfo: 
    The Base EFI contains two config.plist depending on which SMBIOS you choose.  Rename the SMBIOS you prefer to 'config.plist' and delete the other one.  
    You will need to create your own Serial Number and SMUUID.  Instructions can be found [here](https://dortania.github.io/OpenCore-Desktop-Guide/config-HEDT/skylake-x.html#platforminfo)
    * Remember to adjust the Type depending on which SMBIOS you are using.  Either iMacPro1,1 or MacPro7,1
    * NOTE: MacPro7,1 only works on Catalina and higher.
    * Using your results from GenSMBIOS, adjust the following (replace '[Removed]')
        * `PlatformInfo-Generic`
            * MLB: Board Serial
            * SystemSerialNumber: Serial
            * SystemUUID: SmUUID
3. Post-Install
    * It is highly recommended to create your own USB kext. Please use [this](https://dortania.github.io/USB-Map-Guide/) as a proper guide to map your USB ports.
    
## Changelog:
### OpenCore 0.6.6 (2021.02.04)
Bootloader / Kexts:
* Lilu 1.5.1
* WhateverGreen 1.4.7
* AppleALC 1.5.7
* VirtualSMC 1.2.0
* Updated "Resources" files for OpenCanopy GUI

config.plist Changes:
* Misc -> Boot -> PickerAttributes - 25 (Mouse control in Picker)
* Misc -> Boot -> BootProtect -> OC 0.6.6 replaces with LauncherOption and is defaulted to Full
If you were previously using Bootstrap refer to this [link](https://dortania.github.io/OpenCore-Post-Install/multiboot/bootstrap.html#prerequisites/) for instructions on how to upgrade. My previous EFis had it disabled.
* UEFI -> Drivers -> Added OpenHfsPlus.efi (Note: Commented out)
Note that OpenHfsPlus.efi is now bundled with OpenCore but HfsPlus.efi is still enabled for compatibility reasons and is still faster than OpenHfsPlus.efi.


