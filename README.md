# AMD Ryzen Hackintosh

[![MacOS version](https://img.shields.io/badge/Monterey-12.4-informational.svg)](https://www.apple.com/macos) 
[![OpenCore version](https://img.shields.io/badge/OpenCore-0.7.9-informational.svg)](https://github.com/acidanthera/OpenCorePkg)
[![GitHub](https://img.shields.io/github/license/sileshn/Ryzentosh?style=flat-square)](https://github.com/sileshn/Ryzentosh/blob/master/LICENSE)


## Specification

| Component    | Product Name                                     | Note                                           |
|--------------|--------------------------------------------------|------------------------------------------------|
| CPU          | AMD Ryzen 9 3900X                                | PBO enabled                                    |
| Mainboard    | Gigabyte X570 Aorus Elite                        | F31F BIOS                                      |
| Graphics     | AMD Radeon RX 580 8GB                            |                                                |
| NVMe 1       | Samsung SSD 970 EVO Plus 250GB                   | Ubuntu 22.04 installed                         |
| NVMe 2       | GIGABYTE GP-AG4500G                              | macOS 12.4 installed                           |
| BT/WIFI      | Fenvi T919                                       |                                                ||              |                                                  |                                                |

### One more, check this before you use

In the [config.plist](EFI/OC/config.plist) file, I've replaced the private serial codes into the `EDIT_HERE` words because to keep my personal information safe.

So if you are going to use this, you have to make sure that the `EDIT_HERE` texts are changed to yours. To generate the serial key, please refer to the [Dortania's OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#platforminfo). When you are about to generate one, you should select `MacPro7,1` to properly use your machine.

> - If you are going to convert SMBIOS from **iMacPro1,1** to **MacPro7,1**, make sure that you must logout Apple ID from your current system and regenerate all the SMBIOS details such as MLB, serial number, UUID for MacPro7,1.
> - If your CPU has less than 8 cores, go to `config.plist` file and find "PlatformInfo->Generic" and change the "ProcessorType" from 0 to 1537.

### You got another one you must check

From the recent AMD CPU patch, now we have to specify the CPU core counts to the `algrey - Force cpuid_cores_per_package` nodes. Currently, my EFI setup sets that for the **12-core** CPU model because I'm using Ryzen 3900X.

- `algrey - Force cpuid_cores_per_package`
  - 10.13,10.14
    - B8**0C**0000 0000
  - 10.15,11.0
    - BA**0C**0000 0000
  - 12.0
    - BA**0C**0000 0090

Please refer to [the author's description](https://github.com/AMD-OSX/AMD_Vanilla#read-me-first) to get further information.


### OpenCore

- Version: 0.7.9

### ACPI

- SSDT-EC-USBX-DESKTOP.aml - Fixes embedded controller and USB power properties
- SSDT-HPET.aml - Fixes IRQ conflicts
- SSDT-NVME.aml - Makes NVMe drives shown as an internal storage
- SSDT-PLUG.aml - Fixes CPU power management
- SSDT-SBRG.aml - Fixes EC, RTC, IRQ conflicts
- SSDT-SBUS-MCHC.aml - Fixes SMBus support
- SSDT-SBUS-MCHC.aml
- SSDT-XHC.aml - Fixes USB ports mapping

### Drivers

- CrScreenshotDxe.efi
- HfsPlus.efi
- OpenCanopy.efi
- OpenHfsPlus.efi
- OpenNtfsDxe.efi
- OpenRuntime.efi


### Kexts

- AGPMInjector.kext
- AirportItlwm.kext
- AMDRyzenCPUPowerManagement.kext
- AppleALC.kext
- AppleIGB.kext (have bug: lost connection)
- AppleMCEReporterDisabler.kext
- BlueToolFixup.kext
- CtlnaAHCIPort.kext
- DebugEnhancer.kext
- IntelBluetoothFirmware.kext
- IntelBluetoothInjector.kext
- Lilu.kext
- LucyRTL8125Ethernet.kext (disabled)
- NVMeFix.kext
- RadeonSensor.kext
- RealtekRTL8111.kext (disabled)
- RestrictEvents.kext
- SmallTreeIntel82576.kext (disabled)
- SMCAMDProcessor.kext
- SMCRadeonSensor.kext
- VirtualSMC.kext
- WhateverGreen.kext

### Tools

- OpenShell.efi
