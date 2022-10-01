# OpenCore_ASUS_PN62_i7-10510U
This repository contains the files and scripts to install macOS on the ASUS PN62 Desktop Mini PC 65W.

ASUS PN62 Desktop Mini PC

## Hardware Specs

* CPU: Intel(R) Core(TM) i7-10510U CPU
* GPU: Integrated Intel® HD Graphics 620 (2 DisplayPorts + 1 HDMI Port)
* Product Name: ASUS PN62 Desktop Mini PC 65W
* System BIOS: 1005
* Memory: 32 GB DDR4-2666
* LAN: Intel® I219M Gigabit Network Connection LOM
* Audio: Realtek ALC255 Audio (1 front CITA port)

## BIOS Settings

Advanced -> Boot Options

Disable Fast Boot
Disable CD-ROM Boot
Enable USB Storage Boot
Disable Network (PXE) Boot
UEFI & Legacy Boot order, is up to you.
Advanced -> Secure Boot Configuration

Select Legacy Support Enable and Secure Boot Disable
Everything else unchecked.
Advanced -> System Options

Enable Turbo-boost
Enable Hyperthreading
Enable Multi-processor
Enable Virtualization Technology (VTx)
Disable Virtualization Technology for Directed I/O (VTd)
Enable M.2 WLAN/BT
Enable M.2 SSD
Enable Allow PCIe/PCI SERR# Interrupt
Advanced -> Built-in Device Options

Enable Embedded LAN Controller
Disable Wake on LAN
Disable Dust Filter
Video memory size 64MB
Enable M.2 USB / Bluetooth
Enable Audio Device
Enable Internal Speakers
Increase Idle Fan Speed (%), set at 0
Advanced -> Port Options

Everything Enabled
Restrict USB Devices Allow all USB Devices
Advanced > Option ROM Launch Policy

Configure Option ROM Launch Policy All UEFI
Advanced -> Power Management Options

Runtime Power Management Enable
Extended Idle Power States Enable
S5 Maximum Power Savings Disable
SATA Power Management Enable
PCI Express Power Managment Disable (if enabled, it will really screw that native BCM M.2 WiFi performance)
Power On from Keyboard Ports Disable
Unique Sleep State Blink Rates Disable
Advanced -> Remote Management Options

I have not touched anything in here, running defaults AFAIK..
Press F10 to save changes.

Current OS

macOS Monterey 12.4
Bootloader / Kexts

OpenCore v0.8.1
AppleALC
CPUFriend.kext
IntelMausi.kext
Lilu.kext
RTCMemoryFixup.kext
SMCProcessor.kext
SMCSuperIO.kext
USBPorts.kext
VirtualSMC.kext
WhateverGreen.kext
How Install

Follow the instructions at https://dortania.github.io/OpenCore-Install-Guide/installer-guide/ in order to create your macOS installation media and then add the provided EFI folder in this repository.

## iServices (iMessage, iCloud etc) and FileVault

In order to have iServices you need to change a few keys in your config.plist:

ApECID
MLB
ROM
SystemSerialNumber
SystemUUID
Please refer to the following guides to know what needs to be done:

https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-gensmbios
https://dortania.github.io/OpenCore-Post-Install/universal/security/filevault.html
## Known Issues

VGA port - black screen
Can't change the DP port I'm using after the machine is ON - results in a black screen
Can't boot without a screen connected
Sleep doesn't work. Black screen and system crash after trying to wake it up
4K Screen not working correctly
Front Headphone/Mic combo jack is not working, headphone port works, and the combo jack works as line-in
## About Sleep

sudo pmset autopoweroff 0
sudo pmset powernap 0
sudo pmset standby 0
sudo pmset proximitywake 0
sudo pmset tcpkeepalive 0
This is a cautionary tale from someone who spent way more time than anyone should, sleep it's most likely never going to happen. Feel free to prove me wrong! :)

## About the RTC Fix

My current RTC exclusion list is defined permanently in the key rtc-blacklist as described here https://dortania.github.io/OpenCore-Post-Install/misc/rtc.html.

The original value (unexpanded, stored in boot-args) was rtcfx_exclude=58-89,b0-b7,d0-df.

Important note: it seems that every BIOS update needs retesting because it might require the exclusion of additional addresses.
