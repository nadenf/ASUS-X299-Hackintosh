# ASUS X299 Hackintosh

# Introduction
The ASUS X299 Hackintosh repo contains OpenCore EFI distributions and related files that can be used as a reference when starting or migrating your X299 Hackintosh to OpenCore.  While the EFIs can be used as a starting point and should be compatible with all ASUS X299 boards, it is still highly recommended to review the [OpenCore Vanilla Desktop Guide](https://dortania.github.io/OpenCore-Install-Guide/) and [Skylake-X section](https://dortania.github.io/OpenCore-Install-Guide/config-HEDT/skylake-x.html) for a proper guide.

# Folders
| Folder | Description |
| :------------- | :---------- |
| BASE-EFI | OpenCore EFIs with the OpenCanary GUI that should be valid for all ASUS X299 boards.|
| Custom BIOS Collection | Contains modified BIOS files that have custom boot logos |
| EFI-Validated-Distributions | Validated EFIs from other users (Please use this as a reference only) | 
| XHC USB Kexts | USB kexts created by users for specific motherboards.  Please use [this](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html) as a proper guide to map your USB ports. |

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
* Intel X550-T2 10 G Ethernet Card
    * EEPROM modded with Sonnet device id
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
* 2.5 G Ethernet
* 10 G Ethernet
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

# Additional Kexts
* [SmallTreeIntel8259x](https://small-tree.com/support/downloads/10-gigabit-ethernet-driver-download-page/) 
  * Enables built-in Intel 10G ethernet ports on the Sage/10G.
  * Install the version compatible with your version of macOS.
  * Ubuntu EEPROM modding in from [MacRumors thread](https://forums.macrumors.com/threads/modify-retail-intel-10gbe-nics-to-use-small-tree-macos-drivers.1968456/) is required for this kext to work.
* [IntelMausi](https://github.com/acidanthera/IntelMausi/releases)
  * Enables ethernet for most intel controllers
* [SmallTreeIntel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases)
  * Enables ethernet for I211 NICs
  * Version 1.3 is for macOS Catalina, Version 1.2.5 is for macOS 10.13 and 10.14
* [AGPMInjector](https://github.com/Pavo-IM/AGPMInjector) 
  * Apple Graphics Power Management injector

# Credits
* Apple : macOS
* [Acidanthera](https://github.com/acidanthera) : OpencorePkg, kexts, etc.
* [Dortania](https://github.com/dortania) : Opencore guide
* [dracoflar](https://github.com/khronokernel) : Modified SSDT-EC-USBX, PLUG, and SBUS-MCHC files, SmallTree 211 patch, SSDT-RTC0 patch for macOS Big Sur
* [Pavo](https://github.com/Pavo-IM) : AGPMInjector
