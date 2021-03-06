# MSI-Prestige-15
- Model A10SC-213RU

# Hardware
|Specifications | Description|
|-|-|
|CPU       | Intel i5-10210U|
|IGPU      | Intel Graphics UHD 620|
|GPU       | Nvidia GTX1650 Max-Q
|Display   | CMN N156HCE-EN1 FHD
|RAM       | 16GB (8x2) Corsair Vengeance 2400|
|ROM       | Samsung 970 EVO 512GB|
|Audio     | Realtek ACL298|
|Wireless  | Intel AX201|

# Bootloaders / OS
**-----OpenCore-----**
- <img src="https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/Screenshot2.png/" width=512>
- OpenCore: v0.6.2
- MacOS: Catalina 10.15.7 / BigSur 11.0
- SMBIOS: MacBook Pro 15.4
- Config: [In repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/OpenCore/config.plist)

- Required efi drivers
  - AudioDxe
  - HFSPlus
  - OpenCanopy
  - OpenRuntime

**------Clover------**
- <img src="https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/Screenshot.png/" width=512>
- Clover: v5122
- MacOS: Catalina 10.15.7
- SMBIOS: MacBook Pro 15.4
- Config: [In repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/Clover/Configs/config.plist)

- Required efi drivers
  - APFSDriverLoader
  - AudioDxe
  - DataHubDxe
  - FSInject
  - HFSPlus
  - OcQuirks **(included in Clover is broken! Need to download separately)** : https://github.com/ReddestDream/OcQuirks/releases
    - OpenRuntime **(included in Clover is broken!)**
    - OcQuirks.plist [from repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/blob/master/Clover/Configs/OcQuirks.plist)

# ACPI Tables
- [In repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/tree/master/ACPI/patched)

# Required kexts
- Lilu : https://github.com/acidanthera/Lilu/releases
- WhateverGreen : https://github.com/acidanthera/WhateverGreen/releases (version 1.4.6 requires a boot argument *-igfxblr* to enable the display backlight after startup)
- VirtualSMC : https://github.com/acidanthera/VirtualSMC/releases
  - SMCBatteryManager
  - SMCLightSensor
  - SMCProcessor
  - SMCSuperIO
- AppleALC (layout 22) : https://github.com/acidanthera/AppleALC/releases
- NVMeFix : https://github.com/acidanthera/NVMeFix/releases
- NoTouchID : https://github.com/al3xtjames/NoTouchID/releases
- USBPorts.kext [from repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/tree/master/Kexts) (or USBInjectAll : https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads)
- Voodool2C : https://github.com/VoodooI2C/VoodooI2C/releases
  - Voodool2CHID
- VoodooPS2Controller : https://github.com/acidanthera/VoodooPS2/releases
- itlwm : https://github.com/OpenIntelWireless/itlwm/releases
- IntelBluetoothFirmware : https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases
  - IntelBluetoothInjector
- CPUFriend : https://github.com/acidanthera/CPUFriend/releases
  - CPUFriendDataProvider [from repository](https://github.com/KerKerOgh/MSI-Prestige-15-Hackintosh/tree/master/Kexts) 

# Pre-Install
- Make bootable USB Drive with 
  - OpenCore v0.6.2 \- https://github.com/acidanthera/OpenCorePkg/releases
  - or
  - Clover v5122 \- https://github.com/CloverHackyColor/CloverBootloader/releases
  
- Installation requires an internet connection, you have two options:
  - 1. Use usb WI-FI dongle OR usb ethernet adapter
  - 2. Fill your WI-FI SSID and password in itlwm.kext/Contents/Info.plist "WiFiConfig" section

- In BIOS
  - Turn off Secure Boot
  - Press L-ALT + R-CTRL + R-SHIFT + F2 or (fn + F2) for see hidden feature
  - Go to Advanced->Power & Performance->CPU - Power Management Control->CPU lock Configuration->CFG lock = **Disabled**

# Installation
- Install

# Post-Install
- Disable Force Click in trackpad settings for normal left click
- Swap keys: Command -> Option and Option -> Command in keyboard settings
- In Terminal
  - sudo pmset powernap 0
  - sudo pmset proximitywake 0
- Install HeliPort.app to work with internal Wi-Fi \- https://github.com/OpenIntelWireless/HeliPort/releases
- Configure your SMBIOS:
    - OpenCore: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#platforminfo
    - Clover: https://www.tonymacx86.com/threads/guide-how-to-configure-your-systems-smbios-correctly.198155/

# Working
- CPU (800 MHz - 4.20 GHz | 35W | Speed Shift)
- IGPU Intel UHD 620
- WI-FI (HeliPort)
- Bluetooth
- Keyboard (backlight, volume +/-/mute, brightness +/-)
- Trackpad (gestures, prtscr - on/off)
- Audio (AppleALC layout=22)
  - Stereo microphones [**(Bug 1)**](#Bugs)
  - Audio speakers
  - Combined audio jack (Audio+Mic)
- Screen brightness
- Sleep (hibernatemode 3)
- USB 3.2 XHCI Host Controller 
  - Left side 2x USB3.2 Type-C Gen1
  - Right side 2x USB3.2 Gen1
- WebCamera
- Battery indication
- HDMI (Video+Audio) [**(Bug 2)**](#Bugs)
- External monitor (Video+Audio) via Type-C to HDMI adapter  

# Bugs
- Bug 1: Inverted channels
- Bug 2: Green screen after start. Send your laptop to sleep mode and then pull it out, after that everything will work.

# Does not work
- Card Reader Realtek RTS5250 PCI-E
- Fingerprint Reader Synaptics WBDI
- Nvidia GTX1650 Max-Q (Disabled via SSDT)

# Addition
It was helpful:
- https://dortania.github.io/getting-started/
- https://github.com/ErrorErrorError/msi-gs65-gs75-hackintosh#fix-sleep-and-prevent-ddgpu-turning-back-on-after-sleep
- https://github.com/hla63/Msi-modern-15-Hackintosh
