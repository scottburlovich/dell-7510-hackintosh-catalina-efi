# Dell Precision 7510 - MacOS Catalina Bootpack for Clover

This documentation is written assuming that you are already familiar with the process of setting up the [Clover](https://github.com/CloverHackyColor/CloverBootloader/releases) bootloader and installing MacOS on unofficial hardware. If this is not the case, please familiarize yourself with these processes as no support will be provided for them.

Bootpack has been customized for Dell Precision 7510's with the following key specs:

- Intel i7 6820HQ (Skylake)
- Intel HD530 iGPU
- AMD HD 8890M / R9 M275X/M375X dGPU (currently non-functional)
- Intel AC 8260 Wifi/Bluetooth combo adapter

Intel AC 8260 is now **fully operational** thanks to the `itlwm` and `IntelBluetoothFirmware` packages created by the [OpenIntelWireless](https://github.com/OpenIntelWireless) project. Please ensure that you install [HeliPort](https://github.com/OpenIntelWireless/HeliPort ) once your OSX installation is operational in order to configure and manage your wifi connections. 

## Installation

Install [Clover](https://github.com/CloverHackyColor/CloverBootloader/releases) **v5127 or higher**, then place the contents of this bootpack into the `/EFI` folder within your boot partition and **replace** any existing files.

## Installation Notes

**IMPORTANT: dGPU must be disabled**

You must disable the dGPU in your Precision 7510 and increase the DVMT allocation to the iGPU before you can install or run OSX. Failure to do so will result in a kernel panic during boot. Unfortunately, Dell has neglected to allow these settings to be adjusted in their BIOS... so a special tool must be used to make this change by editing the BIOS configuration via UEFI.

Inside the /`DELL PRECISION IGPU` folder, you will find a separate EFI boot environment. Add a new UEFI boot option within the BIOS which targets `/DELL PRECISION IGPU/boot/bootx64.efi`, then boot from this new option by using the boot menu (F12). Once booted, quickly press the right or left arrow key once you see the menu so the default option is not auto-selected. Select `iGPU only` and hit the enter key to disable the dGPU and increase the DVMT allocation for the iGPU. If at some point you need to reverse this change, you can boot this tool again and select the `iGPU+dGPU (default)` option from the menu. If you do happen to find yourself in a situation where the laptop is not able to boot after making this change, try removing the CMOS battery and holding down the power button for 15 seconds. 

**DISCLAIMER**:

Modifying raw BIOS data may cause your computer to become inoperative if performed incorrectly - you are running this tool at your own risk and I will not be held liable for any issues that may arise, nor will I provide any support beyond the above suggestion to clear CMOS.