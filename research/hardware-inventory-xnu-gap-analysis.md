# Hardware inventory and XNU gap analysis — Moto G60 XT2135-2

**Research date:** 2026-11-04  
**Firmware reported by owner:** Android 12, `S2RIS32.32-20-9-9-2-3`  
**Kernel source tag:** `MMI-S2RIS32.32-20-9-9-2-3`  
**Method:** read-only inspection of Motorola's matching Linux source and Apple's public XNU source  
**Device modification:** none

## Executive summary

The matching Motorola source contains a detailed Hanoip device-tree configuration. It identifies multiple board revisions and describes the display, touchscreen, audio, NFC, camera subsystem, fingerprint-related GPIOs, SAR sensor, battery/thermal configuration and UFS-related setup.

Apple's public XNU source includes ARM64 kernel code, ARM platform-expert initialization, a device-tree handoff into IOKit, and generic IOKit abstractions. In the XNU paths inspected, no Hanoip-specific platform expert or matching Qualcomm peripheral driver was found.

**Conclusion:** the device tree gives us a useful hardware map, but it does not provide XNU drivers. A real port would require board-specific startup/platform support and many drivers. This remains a high-risk, unproven research project.

## 1. Source identity and board-revision caution

Motorola's issue #574 names the exact reported firmware package and marks the source code as published:

- https://github.com/MotorolaMobilityLLC/kernel-msm/issues/574
- Matching source tag: https://github.com/MotorolaMobilityLLC/kernel-msm/releases/tag/MMI-S2RIS32.32-20-9-9-2-3

The matching device-tree overlay files declare:

| Overlay | Device-tree board ID | Meaning in source filename |
|---|---:|---|
| `sdmmagpie-hanoip-evt1-overlay.dts` | `0x4C 0xA100` | EVT1 |
| `sdmmagpie-hanoip-dvt1-overlay.dts` | `0x4C 0xB100` | DVT1 |
| `sdmmagpie-hanoip-dvt2-overlay.dts` | `0x4C 0xB200` | DVT2 |

All declare model `hanoip` and Qualcomm MSM ID `365`.

**Important unknown:** the user's exact physical board revision has not been established. Do not select one overlay just because the phone is XT2135-2. The source tag/build number alone does not identify the fitted board revision.

## 2. Hardware inventory

The descriptions below are what the matching Linux device-tree source configures or references. They are not a live hardware scan of the phone.

| Subsystem | Evidence in matching Motorola source | XNU gap / research status |
|---|---|---|
| CPU / SoC platform | ARM64 Android build configuration; Hanoip overlays use MSM ID 365; Qualcomm platform DTS includes | XNU has generic ARM64 code, but no demonstrated Hanoip platform initialization or validated CPU/SoC support |
| Board identification | Three Hanoip overlays with distinct EVT1/DVT1/DVT2 board IDs | Need identify exact board ID for this handset before variant-specific mapping |
| Display | `hanoi-panel.dtsi` references Tianma ILI7807S 678 / 1080×2460 DSI panel description and DSI power/reset setup | No matching Hanoip display driver or panel integration demonstrated in inspected XNU source |
| Touchscreen | SPI node `tchip,ilitek`; reset GPIO 8, interrupt GPIO 9; SPI up to 12 MHz | No matching Ilitek/Hanoip XNU driver identified |
| Audio | Sound-card model `sm6150-wcd9375-snd-card`; SoundWire interrupt/configuration | No matching Qualcomm/WCD9375 Hanoip XNU audio stack identified |
| Rear/front cameras | Qualcomm camera sensor nodes and CCI, clocks, reset GPIOs, regulators, EEPROM/actuator/flash references | No camera pipeline, sensor drivers or Qualcomm camera integration demonstrated for XNU |
| Fingerprint | Hario fingerprint overlay configures reset/interrupt-related GPIOs (including GPIO 4 and 90) | Exact sensor identity and a matching XNU driver are not established |
| NFC | I2C node `qcom,nq-nci` at address `0x28`, with IRQ/enable/firmware/clock-request GPIOs | No matching XNU NFC driver demonstrated |
| SAR / proximity-related sensing | Sensor overlay references `Semtech,sx933x` on I2C | No matching XNU driver demonstrated |
| Battery / charging / thermal | Battery data includes ATL and SUNWODA MC50 6000mAh profiles; charger and thermal policy configuration | Battery pack variant in this handset is unknown; no matching XNU power/thermal integration demonstrated |
| Storage | Hanoip common overlay adjusts `ufshc_mem`; Android board config includes boot/storage image settings | UFS controller initialization, storage driver and boot-volume integration for XNU remain unproven |
| Power management / clocks / GPIO | Qualcomm TLMM GPIO, regulators, clocks, pinctrl and thermal nodes across overlays | Requires board-specific XNU platform and device drivers; Linux device-tree data is descriptive input, not reusable XNU driver code |
| USB / modem / Wi-Fi / Bluetooth / GNSS | Not fully inventoried in this pass | Must inspect remaining base DTS and vendor interface descriptions; no XNU support claimed |

### Camera module names: treat as candidates, not a final BOM

Comments in the EVT1/DVT1/DVT2 camera overlays mention:
- Rear main: Samsung S5KHM2 / OV64B compatibility note
- Rear depth: OV02B1B
- Rear wide: Samsung S5K4H7
- Front: OV16A1Q and OV32B compatibility note

The overlays also configure multiple sensor positions, regulators, 24 MHz camera clocks, reset pins, Qualcomm camera CCI, EEPROM, actuator and flash nodes.

These comments and alternative names do not prove which exact camera module is fitted to the owner's handset. They need corroboration from the exact board variant and vendor configuration.

## 3. XNU architecture comparison

Apple's public XNU README says XNU combines Mach, BSD components and IOKit, and supports ARM64:

https://github.com/apple-oss-distributions/xnu/blob/main/README.md

Relevant source areas inspected:

- `osfmk/arm/arm_init.c`: ARM/ARM64 early initialization calls platform initialization.
- `pexpert/arm/pe_init.c`: ARM platform-expert initialization; includes the ARM64 board configuration interface and initializes IOKit from the device-tree head.
- `iokit/Kernel/IOStartIOKit.cpp`: initializes the IOKit root nub using the device-tree pointer, then configures and starts IOKit matching.
- `iokit/IOKit/IOPlatformExpert.h`: defines platform-expert interfaces, including interrupt-controller registration and platform functions.
- `osfmk/arm64/machine_routines.c`: ARM64-specific machine routines and board-configuration integration.

This architecture provides frameworks and generic ARM64 mechanisms. It does not automatically provide the board-specific implementation for Qualcomm Hanoip. In the inspected XNU paths, no Hanoip-specific platform expert, Qualcomm device-tree binding layer, or drivers matching the peripherals listed above were identified.

## 4. What can be reused, and what cannot

**Useful as research input**
- Device-tree topology and peripheral relationships
- Board IDs and overlay differences
- GPIO, interrupt, clock and regulator descriptions
- Panel and touchscreen bus information
- Candidate sensor/module names
- Linux driver names and source references for understanding hardware behavior

**Not directly reusable as XNU support**
- Linux kernel drivers
- Linux subsystem APIs and device-model code
- Android HALs and vendor services
- Device-tree nodes by themselves (they do not implement drivers)
- Proprietary firmware blobs without verified licensing and compatibility

The practical route is to use the Linux source as hardware documentation, then independently design and implement XNU-compatible platform code and drivers where technically and legally possible.

## 5. Prioritized XNU gap list

1. **Platform bring-up:** establish a documented ARM64 entry environment, memory map, exception levels, interrupt controller, timers and early console for this board. Boot-chain feasibility is a separate gate and remains unknown.
2. **Board/platform expert:** device-tree parsing, board identity, GPIO/pinctrl, clocks, regulators, reset and power sequencing.
3. **Boot storage:** identify the exact storage controller and determine whether a supported XNU storage path can be implemented.
4. **Display and input:** panel/DSI integration and Ilitek SPI touchscreen support.
5. **Power and thermal:** charger, battery gauge, thermal zones and suspend/resume.
6. **Connectivity and peripherals:** audio, camera/ISP, NFC, fingerprint, SAR/proximity, modem, Wi-Fi, Bluetooth, USB and GNSS.
7. **Operating-system layer:** a usable Darwin/iOS userspace is a separate and much larger problem; XNU alone is not iOS 26.

## 6. Next safe research actions

- Determine which board ID/overlay applies to the exact XT2135-2 revision using existing documentation only.
- Inspect the base Hanoip/Qualcomm DTS for interrupt controller, timer, memory and storage topology.
- Inventory the Linux driver source paths for each major peripheral and record whether specifications are public.
- Compare those interfaces against XNU's public platform and IOKit interfaces.
- Keep the boot-chain question in documentation-only status until authoritative device-specific documentation and a recovery plan exist.

## Safety and scope

This work is read-only source analysis on a computer. No instructions or authorization are provided for flashing, unlocking, repartitioning, replacing boot images or testing experimental boot paths. Do not use proprietary Apple system files, firmware, keys or assets. No genuine iOS 26 port or successful XNU boot on XT2135-2 has been demonstrated.
