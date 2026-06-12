# Hackintosh-Tahoe-Honor-Magicbook-X15-Intel-Comet-Lake
OpenCore Hackintosh EFI configuration for the Honor MagicBook X15 (Intel Comet Lake). Includes comprehensive documentation on working components and physical hardware limitations (Intel SST, HDMI). Open for community contributions.

# Honor MagicBook X15 - OpenCore EFI

OpenCore bootloader configuration for the Honor MagicBook X15. This repository provides a stable base for macOS, with necessary ACPI patches and kexts tailored for this specific Comet Lake architecture. 

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

### Core System
| Component | Status | Notes |
| :--- | :--- | :--- |
| CPU Power Management | Working | Native Intel SpeedStep/Speed Shift. |
| iGPU Acceleration | Working | Full QE/CI via WhateverGreen. |
| Sleep / Wake | Working | |
| NVRAM | Working | Native read/write support. |
| Battery Readout | Working | SMCBatteryManager integration. |

### Input / Output
| Component | Status | Notes |
| :--- | :--- | :--- |
| Internal Keyboard | Working | VoodooPS2Controller. |
| Trackpad (I2C) | Working | Gestures supported via VoodooI2C. |
| USB Ports | Working | Custom USB map applied. |
| Wi-Fi & Bluetooth | Working | Managed via AirportItlwm and IntelBluetoothFirmware. |
| Web Camera | Working | Native USB interface. |

### Audio & Video (Known Quirks)
| Component | Status | Notes |
| :--- | :--- | :--- |
| USB / Bluetooth Audio | Working | Seamless output. |
| Internal Speakers / Mic | Unsupported | Hardware limitation. See section below. |
| HDMI Port | Unsupported | Routing incompatible with macOS framebuffers. |
| Type-C Video Output | Unsupported | Port lacks DisplayPort Alt Mode physically. |

## Hardware Limitations (Important)

Due to specific OEM architectural designs, the following components cannot be enabled through OpenCore configuration or ACPI patching.

**1. Intel Smart Sound Technology (SST)**
The internal Realtek ALC256 audio codec is not routed through a standard High Definition Audio (HDA) bus. It is physically routed through an Intel DSP (`INTELAUDIO\FUNC_01`). AppleHDA lacks the proprietary drivers to communicate with this DSP, rendering the internal speakers and combo jack invisible to the OS.
* *Solution:* Use a Type-C to 3.5mm DAC adapter for wired headsets, or rely on Bluetooth audio.

**2. Video Output**
The physical HDMI port is routed through an internal converter that macOS cannot interface with. Furthermore, the single Type-C port on this machine is wired strictly for USB data and Power Delivery, lacking the physical pins for DisplayPort Alt Mode.
* *Solution:* External monitors must be connected using a USB Type-A adapter featuring **DisplayLink** technology. Standard passive adapters will not work.

## BIOS Configuration

Before booting, ensure the following settings are applied in the BIOS:

* **Secure Boot:** Disabled
* **Fast Boot:** Disabled
* **SATA Mode:** AHCI (if applicable)
* **TPM:** Disabled (Recommended for macOS installation)

## Credits

* [Acidanthera](https://github.com/acidanthera) for OpenCore and core Kexts.
* [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the OpenCore Install Guide.
