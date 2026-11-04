# Moto G60 XT2135-2 device profile

**Project:** iPortMotoG60  
**Target device:** Motorola Moto G60 XT2135-2  
**Research status:** Preliminary; host-side research only  
**Last reviewed:** 2026-11-04

## Identity

- Exact model supplied by the project owner: **XT2135-2**.
- Motorola conformity documentation identifies XT2135-2 as **Moto G60 Vision** in that listing.
- Public Android device trees group Moto G60 and Moto G40 Fusion under the device codename **hanoip**. This family-level codename does not, by itself, prove that every firmware, partition layout, peripheral, or boot detail is identical across model variants.
- The installed software build on this particular handset has not yet been recorded.

## Hardware facts: provisional

Community-maintained Android device trees and recovery metadata report the following for the hanoip family:

| Item | Reported value | Confidence |
|---|---|---|
| SoC family | Qualcomm Snapdragon 732G | Community-source report; confirm against exact XT2135-2 documentation |
| GPU | Adreno 618 | Community-source report |
| CPU architecture | ARM64 | Supported by public Android build configuration |
| Display | 1080-class resolution | Exact panel/resolution needs variant-specific confirmation |
| RAM/storage | Multiple configurations reported | Exact handset configuration unknown |

Do not treat family-level device-tree values as verified XT2135-2 hardware specifications until corroborated by Motorola documentation or variant-specific source.

## Android source references

- Hanoip device tree: https://github.com/motorola-sm6150-devs/device_motorola_hanoip
- Hanoip device configuration: https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/BoardConfig.mk
- Motorola kernel source organization: https://github.com/MotorolaMobilityLLC

The cited device tree is an Android build configuration. Its values describe that Android build target; they do not demonstrate XNU compatibility or prove that a non-Android kernel can be accepted by the handset's boot chain.

## Unknowns to resolve

1. Exact Android build number and security patch level on the XT2135-2.
2. Exact regional software channel and firmware package identity.
3. Which public kernel-source revision corresponds to that firmware build.
4. Variant-specific boot image and device-tree documentation.
5. Verified-boot policy and documented recovery path.
6. Whether any safe, documented boot handoff mechanism exists for this model.

## Project safety boundary

Current work is documentation and source review on a computer. Do not flash images, alter partitions, unlock or modify boot configuration, or experiment with boot images. Preserve the handset's normal working state and recovery options.

## XNU / iOS 26 status

No working XNU port, iOS 26 userspace, device drivers, or successful boot path has been demonstrated for XT2135-2. XNU source alone is not a complete iOS installation; proprietary Apple components and extensive hardware/platform integration would also be involved. Do not redistribute proprietary Apple software, firmware, keys, or assets.
