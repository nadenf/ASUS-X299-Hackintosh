# ASUS X299 Hackintosh

# Introduction
The ASUS X299 Hackintosh repo contains OpenCore EFI distributions and related files that can be used as a reference when starting or migrating your X299 Hackintosh to OpenCore.  While the EFIs can be used as a starting point and should be compatible with all ASUS X299 boards, it is still highly recommended to review the [OpenCore Vanilla Desktop Guide](https://dortania.github.io/OpenCore-Install-Guide/) and [Skylake-X section](https://dortania.github.io/OpenCore-Install-Guide/config-HEDT/skylake-x.html) for a proper guide.

# Folders
| Folder | Description |
| :------------- | :---------- |
| Custom BIOS Collection | Contains modified BIOS files that have custom boot logos |
| BASE-EFI | OpenCore EFIs with the OpenCanary GUI that should be valid for all ASUS X299 boards.  Refer to section [BASE-EFI Configuration](https://github.com/shinoki7/Asus-X299-Hackintosh#base-efi-configuration) for more details. |
| EFI-Validated-Distributions | Validated EFIs from other users (Please use this as a reference only) | 
| XHC USB Kexts | USB kexts created by users for specific motherboards.  Please use [this](https://dortania.github.io/USB-Map-Guide/) as a proper guide to map your USB ports. |

# Personal Build Specifications
![](/Images/aboutthismac.png)
## Components
* Motherboard : ASUS Pro WS X299 Sage II
    * BIOS 0901
* Processor : Intel i9-10980XE
* CPU Cooler : Corsair H150i Pro RGB
* RAM : 4x16 Corsair Dominator Platinum RGB 3200 Mhz
* Boot Drive : Samsung 970 EVO 1 TB
* Graphics Card : Sapphire RX 580 Pulse 8 GB
* Power Supply : Corsair RM 850x
* Case : Lian Li PC 011 Dynamic

## Additional Components / Peripherals
* 2X Gigabyte Titan Ridge Thunderbolt 3 Card 
    * Flashed with custom NVM50 firmware
* Apple Magic Keyboard 2 (Space Gray)
* Apple Magic Trackpad 2 (Space Gray)
* Apple Magic Mouse 2 (Space Gray)
* LG 27UL600 27" 4K UHD Monitor
* LG 27UL600 27" 4K UHD Monitor
* LG 27UK600 27" 4K UHD Monitor
* LG C9 65" 4K UHD TV

## What Works
* Sleep / Wake
* Wifi and Bluetooth (Using natively supported Broadcom BCM943602CDP)
* Handoff, Continuity, AirDrop, Continuity Camera, and Unlock with Apple Watch
* iMessage, FaceTime, App Store, iTunes Store
* Ethernet
* 10Gb Ethernet
* HEVC, H.264
* Onboard audio
* TRIM
* USB 2.0 / USB 3.0
* USB 3.1 Gen 2
* Thunderbolt 3 w/ hot plug including Thunderbolt Local Node and Thunderbolt Bus. Credits @CaseySJ and contributors in his [thread](https://www.tonymacx86.com/threads/success-gigabyte-designare-z390-thunderbolt-3-i7-9700k-amd-rx-580.267551/)
* DRM
* Native NVRAM
* CPU Power Management
* USB Power

## What Doesn't Work
* SideCar due to some T2 chip dependancies on MacPro7,1 and iMacPro1,1 SMBIOS (Using Duet Display as alternative)

## Comments
The ASUS WS X299 Sage series (WS X299 Sage, WS X299 Sage/10G, Pro WS X299 Sage II) are great motherboards with 7 PCIe slots running at 16x/8x/8x/8x/8x/8x/8x and multiple M.2/U.2 connections.  The Sage/10G even includes dual 10Gb Intel X550-AT2 LAN ports that are compatible with macOS. Unfortunately the motherboards only have a few USB ports and only a single 19 Pin USB 3.0 header for internal ports.  In order to connect internal USB devices such as Bluetooth or RGB Controllers there are a few options.  Note that the specific cables/card listed below are examples.  Just make sure the PCIe card is compatible with macOS.
* 1. [USB 3.0 20 Pin Female to USB 2.0 Pin Male Adapter](https://www.amazon.com/gp/product/B01MFB04JP/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
    * With this you will not have a USB 3.0 header to connect to the front of your case
    * Currently using this in my build with a [USB 2.0 9 Pin Header 1 to 4 Extension Hub Splitter](https://www.amazon.com/gp/product/B085KVH16T/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) to connect Bluetooth and the USB 2.0 cables for my 2 thunderbolt 3 cards.
* 2. [USB 2.0 IDC 5 Male to USB A Male adapter](https://www.amazon.com/gp/product/B000V6WD8A/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
    * Uses one of the USB ports on the back of the motherboard to connect internal devices in the case.  You can get two of these and remove 1 of the pins to make a "9 pin internal adapter".  If the cable is too short from the back to inside the case, you can get some regular USB A extension cables.
* 3. PCIe USB 3.0 Card with Internal USB Connector
    * [Inateck USB 3.0 Card](https://www.amazon.com/Inateck-Express-Controller-Internal-Connector/dp/B00JFR2H64/ref=sr_1_3?dchild=1&keywords=inateck+pcie+card&qid=1592455853&s=electronics&sr=1-3)
    * [StarTech USB 3.1 PCIe Card](https://www.amazon.com/gp/product/B01I39D15A/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
    * Can use the internal header on the card for the case USB ports or to connect internal devices.
    * NOTE: Wake from Bluetooth devices does not work with this so it's best to connect Bluetooth to one of the motherboard ports.

# Base EFI Configuration
The Base EFI folder contains a prebuilt EFI that should be valid for all ASUS X299 motherboards.  It is currently built using OpenCore 0.6.0 with the OpenCanary GUI enabled following the Dortania OpenCore Vanilla Guide.

## 1. Important BIOS Settings
* Above 4G Encoding: Enabled
* MSR Lock: Disabled
* CSM: Disabled

## 2. Configuration
1. Ethernet: 
    * For WS X299 Sage/10G users replace IntelMausi with [SmallTreeIntel8259x](https://small-tree.com/support/downloads/10-gigabit-ethernet-driver-download-page/) kext and update the kext entry.  NOTE: Requires Ubuntu EEPROM modding outlined in @KGPs [guide section E.8.2.2](https://www.tonymacx86.com/threads/how-to-build-your-own-imac-pro-successful-build-extended-guide.229353/)
    * For users with I211 NICs like the X299 Deluxe, copy the [SmallTreeIntel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases) kext to your EFI folder and add a new kext entry under `Kernel-Add`
2. TSCAdjustReset:
    * From the Kexts-TSCAdjustReset [folder](https://github.com/shinoki7/Asus-X299-Hackintosh/tree/master/Kexts/TSCAdjustReset), download the zip with the number of cores your processor and extract the file.  Copy this file to your EFI folder under `EFI-OC-Kexts`
4. SSDT-RTC0: 
    * By default, the Base-EFI folder assumes you're on the latest BIOS and has SSDT-RTC0.aml enabled.  If you're on a pre Cascade Lake X motherboard and BIOS version below 3000 (i.e 2002) replace SSDT-RTC0.aml in your EFI folder with [SSDT-RTC0-NOAWAC.aml](https://github.com/shinoki7/Asus-X299-Hackintosh/blob/master/SSDT/SSDT-RTC0-NOAWAC.aml) and rename to SSDT-RTC0.aml
5. CFG Lock:
    * By default, the Base-EFI folder assumes you're on the latest BIOS. 
6. PlatformInfo: 
    You will need to create your own Serial Number and SMUUID.  Instructions can be found [here](https://dortania.github.io/OpenCore-Desktop-Guide/config-HEDT/skylake-x.html#platforminfo)
    * Remember to adjust the Type depending on which SMBIOS you are using.  Either iMacPro1,1 or MacPro7,1
    * NOTE: MacPro7,1 only works on Catalina and higher.
    * Using your results from GenSMBIOS, adjust the following (replace '[Removed]')
        * `PlatformInfo-Generic`
            * MLB: Board Serial
            * SystemSerialNumber: Serial
            * SystemUUID: SmUUID
6. Post-Install
    * It is highly recommended to create your own USB kext. Please use [this](https://dortania.github.io/USB-Map-Guide/) as a proper guide to map your USB ports.

# Additional Kexts
* [SmallTreeIntel8259x](https://small-tree.com/support/downloads/10-gigabit-ethernet-driver-download-page/) 
  * Enables built-in Intel 10G ethernet ports on the Sage/10G.
  * Install the version compatible with your version of macOS.
  * Ubuntu EEPROM modding in @KGPs [guide section E.8.2.2](https://www.tonymacx86.com/threads/how-to-build-your-own-imac-pro-successful-build-extended-guide.229353/) is required for this kext to work.
* [IntelMausi](https://github.com/acidanthera/IntelMausi/releases)
  * Enables ethernet for most intel controllers
* [SmallTreeIntel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases)
  * Enables ethernet for I211 NICs
  * Version 1.3 is for macOS Catalina, Version 1.2.5 is for macOS 10.13 and 10.14
* [AGPMInjector](https://github.com/Pavo-IM/AGPMInjector) 
  * Apple Graphics Power Management injector
  
# macOS Big Sur Installation
Refer to [Dortania Big Sur Section](https://dortania.github.io/OpenCore-Install-Guide/extras/big-sur/) for more information and known issues.

# Credits
* Apple : macOS
* [Acidanthera](https://github.com/acidanthera) : OpencorePkg, kexts, etc.
* [Dortania](https://github.com/dortania) : Opencore guide
* [dracoflar](https://github.com/khronokernel) : Modified SSDT-EC-USBX, PLUG, and SBUS-MCHC files, SmallTree 211 patch, SSDT-RTC0 patch for macOS Big Sur
* [Pavo](https://github.com/Pavo-IM) : AGPMInjector
