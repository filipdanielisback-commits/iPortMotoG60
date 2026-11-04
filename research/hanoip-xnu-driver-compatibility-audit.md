# Hanoip hardware-to-XNU driver compatibility audit

**Research date:** 2026-11-04  
**Target:** Motorola Moto G60 XT2135-2 (Hanoip family)  
**Reported software:** Android 12, build `S2RIS32.32-20-9-9-2-3`  
**Motorola source revision:** `MMI-S2RIS32.32-20-9-9-2-3`  
**XNU reference:** `xnu-12377.1.9` (iOS 26-era candidate; not an Apple-confirmed universal iOS 26 mapping)  
**Method:** read-only inspection of public source files and repository directory listings  
**Device changes:** none

## Executive finding

The Motorola Linux source provides substantial evidence about Hanoip hardware: ARM64 build configuration, board overlays, a DSI panel, Ilitek SPI touchscreen, WCD9375 audio configuration, NFC and sensor nodes, camera topology, UFS configuration, and a vendor module list containing audio, fingerprint, USB-network and WLAN modules.

The inspected public XNU source provides generic ARM64 startup, platform-expert and IOKit infrastructure. Its inspected `iokit/Families` directory contains only `IONVRAM` and `IOSystemManagement`; the `iokit/DriverKit` directory contains interface definitions rather than a Hanoip driver pack. Searches of the XNU repository for `hanoip` and Qualcomm IOKit driver matches returned no results.

**No matching Hanoip-specific XNU platform expert or peripheral-driver implementation was identified in this audit.** This is a bounded source audit, not proof that no relevant code exists anywhere in Apple's private source or other separately published repositories.

## Status definitions

- **Partial framework:** XNU has generic architecture or subsystem abstractions, but no demonstrated Hanoip implementation.
- **No match found:** no matching implementation was located in the inspected public XNU source paths/searches.
- **Unknown:** the hardware identity or required interface has not been established sufficiently.
- **Linux evidence only:** Motorola's Linux source documents a component, but this does not establish XNU support.

These labels describe source research, not device test results.

## Compatibility matrix

| Hardware / subsystem | Motorola evidence | XNU audit result | Status |
|---|---|---|---|
| ARM64 CPU startup | Hanoip Android BoardConfig selects `arm64`; Motorola kernel source is Linux 4.14.190 | XNU contains generic ARM64 startup and machine code; no validated Hanoip entry/boot contract | Partial framework |
| Hanoip board identity | Motorola source has EVT1, DVT1 and DVT2 overlays with different board IDs; exact handset revision unknown | No Hanoip-specific platform expert located | No match found |
| Device tree / platform expert | Linux overlays describe hardware and board-specific GPIOs, regulators and devices | XNU has generic ARM platform-expert and device-tree-to-IOKit initialization paths; no Hanoip binding implementation found | Partial framework |
| Interrupt controller, timers, clocks, GPIO, regulators | Qualcomm/Linux DTS includes these platform resources | Generic XNU abstractions exist, but exact Hanoip controller drivers and initialization are not demonstrated | Unknown / no match found |
| UFS storage | Motorola common overlay configures UFS PHY/controller nodes | No Hanoip UFS controller driver or verified boot-volume path identified in inspected XNU source | No match found |
| Display | `hanoi-panel.dtsi` references Tianma ILI7807S 678, 1080×2460 DSI panel and power/reset sequence | No matching Qualcomm DSI host + Hanoip panel integration identified in inspected XNU source | No match found |
| Touchscreen | Device tree uses `tchip,ilitek` on SPI; reset GPIO 8, IRQ GPIO 9 | No matching Ilitek/Hanoip IOKit driver found in inspected source | No match found |
| Audio | Device tree sets model `sm6150-wcd9375-snd-card`; Android module list includes Qualcomm audio modules | No matching WCD9375/SoundWire Hanoip XNU audio stack identified | No match found |
| Cameras | Hanoip overlay includes camera-sensor DTSI; sensor candidates and CCI, clocks, reset/regulator resources are described | No matching Qualcomm camera pipeline or Hanoip camera drivers identified | No match found |
| Fingerprint | Android module list includes `fpsensor_spi_tee.ko`; a fingerprint overlay configures GPIO resources | Exact sensor/TEE interface is not established; no matching XNU driver found | Unknown / no match found |
| NFC | Hanoip overlay references `qcom,nq-nci` over I2C | No matching NFC driver located in inspected XNU source | No match found |
| SAR / proximity-related sensor | Sensor overlay references `Semtech,sx933x` over I2C | No matching SX933x/Hanoip driver identified | No match found |
| Battery / charging / thermal | Motorola DTS includes battery profiles, charger configuration and thermal policy | No Hanoip-specific power/thermal implementation identified | No match found |
| Wi-Fi | Android module list includes `qca_cld3_wlan.ko` | Exact chipset/interface and matching XNU driver are not established | Unknown |
| Bluetooth | Not established from the files inspected in this pass | No matching Hanoip Bluetooth driver identified | Unknown |
| Cellular modem / telephony | Not fully inventoried from the inspected files | Modem firmware, transport, power sequencing and telephony integration are not established | Unknown |
| USB | BoardConfig includes USB controller command-line setting; module list includes `moto_f_usbnet.ko` | No matching Hanoip USB controller/peripheral implementation identified | Unknown / no match found |
| GNSS | Not fully inventoried in this pass | No matching GNSS driver or service path identified | Unknown |
| Sensors beyond SX933x | Vendor module list includes `sensors_class.ko`; exact sensor inventory remains incomplete | No complete sensor stack mapped to XNU | Unknown |

## Evidence inspected

### Motorola device build configuration

The community Hanoip Android device tree's `BoardConfig.mk` sets:
- `TARGET_ARCH := arm64`
- `TARGET_BOARD_PLATFORM := sm6150`
- `TARGET_BOOTLOADER_BOARD_NAME := hanoip`
- kernel source path `kernel/motorola/sm6150`
- Android boot header version 3
- separate DTBO and DTB-in-boot-image settings
- AVB enabled

These are Android/Linux build properties. They are not an XNU boot specification.

Source: [Hanoip BoardConfig.mk](https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/BoardConfig.mk)

### Android vendor kernel modules

The Hanoip `modules.load` file includes, among others:
- Qualcomm audio modules, including WCD937x-related modules
- `fpsensor_spi_tee.ko`
- `moto_f_usbnet.ko`
- `qca_cld3_wlan.ko`
- `sensors_class.ko`

This is evidence of Linux-side modules in that Android device tree. It does not establish the exact Wi-Fi chipset, the exact fingerprint sensor identity, or corresponding XNU drivers.

Source: [Hanoip modules.load](https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/modules.load)

### Matching Motorola kernel source

- [Exact Motorola source tag](https://github.com/MotorolaMobilityLLC/kernel-msm/tree/MMI-S2RIS32.32-20-9-9-2-3)
- [Hanoip DVT2 overlay](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-dvt2-overlay.dts)
- [Motorola common overlay](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-moto-common-overlay.dtsi)
- [Hanoi touchscreen description](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoi-touchscreen.dtsi)
- [Hanoi panel description](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/hanoi-panel.dtsi)
- [Audio overlay](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-audio-overlay.dtsi)
- [Hanoip sensor overlay](https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-sensor-overlay.dtsi)

The DVT2 overlay is linked as one source example only. The owner's actual board revision is still unknown; this audit does not assert that DVT2 is the correct overlay for the handset.

### Apple XNU source

- [Apple XNU repository](https://github.com/apple-oss-distributions/xnu)
- [Candidate XNU tag xnu-12377.1.9](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9)
- [XNU ARM platform-expert source](https://github.com/apple-oss-distributions/xnu/blob/xnu-12377.1.9/pexpert/arm/pe_init.c)
- [XNU IOKit startup source](https://github.com/apple-oss-distributions/xnu/blob/xnu-12377.1.9/iokit/Kernel/IOStartIOKit.cpp)
- [XNU IOKit directory](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9/iokit)
- [XNU IOKit Families directory](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9/iokit/Families)
- [XNU DriverKit interface directory](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9/iokit/DriverKit)

The inspected `iokit/Families` directory contains `IONVRAM` and `IOSystemManagement`. DriverKit contains interface definitions and related headers; that is not evidence of Hanoip device drivers. Repository searches for `hanoip` and Qualcomm IOKit driver matches returned no results.

## Key conclusions

1. **Generic ARM64 support is not board support.** XNU's ARM64 code does not automatically initialize this Motorola board.
2. **Linux DTS is hardware documentation, not portable driver code.** It describes buses, GPIOs, clocks, regulators, interrupts and components; XNU needs its own compatible implementations.
3. **The largest visible gaps are platform bring-up, storage, display, touch, audio, camera, power, wireless and modem integration.**
4. **Some component identities remain unknown.** Wi-Fi chipset, Bluetooth path, modem interface, GNSS and exact fingerprint/camera module variants require further evidence.
5. **The exact physical board revision is still unknown.** Do not choose an EVT/DVT overlay based on model name alone.
6. **No boot feasibility has been demonstrated.** This audit does not justify flashing, unlocking, repartitioning or testing experimental images.

## Next research milestone

Before any device-side work, investigate the Hanoip base device tree and Linux driver source paths for the boot-critical platform pieces: memory map, GIC/interrupt controller, timers, clocks, pinctrl/GPIO, regulators, UFS and USB. Then compare each interface with the relevant public XNU abstraction and identify what would need a new implementation. Continue to keep all work read-only and non-destructive.

## Scope and licensing

This is a source-inspection report, not a port. Do not copy proprietary Apple operating-system files, firmware, signing keys, leaked material, or vendor blobs into this repository. Respect the licenses of both Apple and Motorola/community source material.
