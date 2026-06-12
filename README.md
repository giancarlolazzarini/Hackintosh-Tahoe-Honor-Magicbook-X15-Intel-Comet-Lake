# Honor MagicBook X15 - OpenCore EFI

OpenCore bootloader configuration for the Honor MagicBook X15. This repository provides a base for macOS, tailored for this specific Comet Lake architecture. 

Please read the hardware limitations section carefully before deploying this EFI.

## Hardware Specifications

| Component | Specification |
| :--- | :--- |
| **Model** | Honor MagicBook X15 |
| **CPU** | Intel Core (Comet Lake) |
| **iGPU** | Intel UHD Graphics |
| **RAM** | DDR4 (Soldered) |
| **Storage** | NVMe SSD |
| **Audio** | Realtek ALC256 (Intel SST Routed) |
| **Trackpad** | I2C Interface |

## Component Status

| Component | Yes | WIP | No | Notes |
| :--- | :---: | :---: | :---: | :--- |
| iGPU Acceleration | ✓ | | | Full QE/CI via WhateverGreen. |
| Wi-Fi & Bluetooth | ✓ | | | Managed via AirportItlwm and IntelBluetoothFirmware. |
| Trackpad (I2C) & Keyboard | ✓ | | | Gestures supported; VoodooPS2Controller integration. |
| USB Ports & Web Camera | ✓ | | | Custom USB map applied; Native camera interface. |
| Sleep/Wake & NVRAM | ✓ | | | Native power states and read/write support. |
| CPU Power Management | | ✓ | | Configuration currently in progress. |
| Internal Audio (ALC256) | | | ✓ | Hardware limitation (Intel SST routed). |
| HDMI Port | | | ✓ | Routing incompatible with macOS framebuffers. |

## Hardware Limitations

**1. Intel Smart Sound Technology (SST)**
The internal Realtek ALC256 audio codec is routed through an Intel DSP (`INTELAUDIO\FUNC_01`). AppleHDA lacks the proprietary drivers to communicate with this DSP.
* *Workaround:* Use a Type-C to 3.5mm DAC adapter for wired headsets, or rely on Bluetooth audio.

**2. Video Output**
The physical HDMI port is routed through an internal converter that macOS cannot interface with. The single Type-C port is wired strictly for USB data and Power Delivery.
* *Workaround:* External monitors must be connected using a USB Type-A adapter featuring DisplayLink technology.

## BIOS Configuration

* **Secure Boot:** Disabled
* **Fast Boot:** Disabled
* **TPM:** Disabled

## Credits

* [Acidanthera](https://github.com/acidanthera) for OpenCore and core Kexts.
* [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the OpenCore Install Guide.
