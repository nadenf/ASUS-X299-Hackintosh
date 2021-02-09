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
| Component        | Model                                |
| ---------------- | ---------------------------------------|
| Motherboard | ASUS Pro WS X299 Sage II |
| Processor | Intel i9-10980XE |
| CPU Cooler | Corsair H150i Pro RGB |
| RAM | 4x16 Corsair Vengeance LPX 3200 Mhz |
| Boot Drive | Samsung 970 EVO 1 TB |
| Graphics Card | Sapphire RX 580 Pulse 8 GB |
| Power Supply | Corsair RM 850x |
| Case | Lian Li PC 011 Dynamic |

## What Works / What Doesn't Work
- [x] Sleep / Wake
- [x] Wifi and Bluetooth (Using natively supported Broadcom BCM943602CDP)
- [x] Handoff, Continuity, AirDrop, Continuity Camera, and Unlock with Apple Watch
- [x] iMessage, FaceTime, App Store, iTunes Store
- [x] 2.5 G Ethernet
- [x] HEVC, H.264
- [x] Onboard audio
- [x] TRIM
- [x] USB 2.0 / USB 3.0
- [x] USB 3.1 Gen 2
- [x] DRM
- [x] Native NVRAM
- [x] CPU Power Management
- [x] USB Power
- [ ] SideCar due to some T2 chip dependancies on MacPro7,1 and iMacPro1,1 SMBIOS (Using Duet Display as alternative)

## BIOS Settings
* Based off Pro WS X299 Sage II on BIOS 0901 but should be valid for any Asus X299 Motherboard running the latest BIOS.
* Reset to Default Settings before changing these settings

### AI Tweaker
* AI Overclock Tuner - Enabled

### Advanced
#### CPU Configuration
* MSR Lock Control - **[Disabled]**
    ##### CPU Power Management Configuration
    * Enhanced Intel SpeedStep Technology - Enabled
    * Turbo Mode - Enabled
    * Autonomous Core C-State - Enabled
    * Enhanced Halt State (C1E) - Enabled
    * CPU C6 Report - Enabled
    * Package C State - C6(non Retention) state
    * Intel(R) Speed Shift Technology - Enabled
    * MFC Mode Override - OS Native Support
#### System Agent (SA) Configuration
* Intel VT for Directed I/O (VT-d) - Enabled
#### PCH Storage Configuration
* SATA Mode Selection - AHCI

### Boot
* Above 4G Decoding - **[On]**
#### CSM (Compatability Support Module)
* Launch CSM - **[Disabled]**
#### Secure Boot
* OS Type - Other OS

## Comments
The ASUS WS X299 Sage series (WS X299 Sage, WS X299 Sage/10G, Pro WS X299 Sage II) are great motherboards with 7 PCIe slots running at 16x/8x/8x/8x/8x/8x/8x and multiple M.2/U.2 connections.  The Sage/10G even includes dual 10Gb Intel X550-AT2 LAN ports that are compatible with macOS. Unfortunately the motherboards only have a few USB ports and only a single 19 Pin USB 3.0 header for internal ports.  In order to connect internal USB devices such as Bluetooth or RGB Controllers there are a few options.  Note that the specific cables/card listed below are examples.  Just make sure the PCIe card is compatible with macOS.
* 1. [USB 3.0 20 Pin Female to USB 2.0 Pin Male Adapter](https://www.amazon.com/gp/product/B01MFB04JP/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
    * This adapter converts the internal USB 3.0 19 pin header to a USB 2.0 9 pin.
    * Currently using this in my build with a [USB 2.0 9 Pin Header 1 to 4 Extension Hub Splitter](https://www.amazon.com/gp/product/B085KVH16T/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) to connect Bluetooth.
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
