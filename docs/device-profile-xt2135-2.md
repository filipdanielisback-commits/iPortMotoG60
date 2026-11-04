# Moto G60 XT2135-2 device profile

**Project:** iPortMotoG60  
**Target device:** Motorola Moto G60 XT2135-2  
**Reported Android version:** Android 12  
**Reported build number:** `S2RIS32.32-20-9-9-2-3`  
**Research status:** Preliminary; host-side research only  
**Last reviewed:** 2026-11-04

## Identity and installed software

- Exact model supplied by the project owner: **XT2135-2**.
- Motorola conformity documentation identifies XT2135-2 as **Moto G60 Vision** in that listing.
- The owner reports Android 12 and build `S2RIS32.32-20-9-9-2-3`.
- Motorola's issue #574 links a published kernel source release for the exact XT2135-2 build string. The matching release tag is `MMI-S2RIS32.32-20-9-9-2-3`; its root Makefile was inspected and identifies Linux 4.14.190. This confirms a matching Linux source release exists, but does not establish a successful build or XNU compatibility.
- Public Android device trees group Moto G60 and Moto G40 Fusion under the device codename **hanoip**. This family-level codename does not, by itself, prove that every firmware, partition layout, peripheral, or boot detail is identical across model variants.

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

## Android and kernel source references

- Hanoip device tree: https://github.com/motorola-sm6150-devs/device_motorola_hanoip
- Hanoip device configuration: https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/BoardConfig.mk
- Motorola kernel source organization: https://github.com/MotorolaMobilityLLC
- Motorola kernel source issue referencing XT2135-2 build `S2RIS32.32-20-9-9-2-3`: https://github.com/MotorolaMobilityLLC/kernel-msm/issues/574
- Matching published kernel source tag: https://github.com/MotorolaMobilityLLC/kernel-msm/releases/tag/MMI-S2RIS32.32-20-9-9-2-3
- Detailed kernel/XNU comparison: [research/kernel-xnu-comparison.md](../research/kernel-xnu-comparison.md)

The cited device tree is an Android build configuration. Its values describe that Android build target; they do not demonstrate XNU compatibility or prove that a non-Android kernel can be accepted by the handset's boot chain.

## Unknowns to resolve

1. Exact regional software channel and firmware package identity.
2. Which Hanoip board overlay corresponds to this exact handset's hardware revision.
3. Variant-specific boot image and device-tree documentation.
4. Verified-boot policy and documented recovery path.
5. Whether any safe, documented boot handoff mechanism exists for this model.

## Project safety boundary

Current work is documentation and source review on a computer. Do not flash images, alter partitions, unlock or modify boot configuration, or experiment with boot images. Preserve the handset's normal working state and recovery options.

## XNU / iOS 26 status

No working XNU port, iOS 26 userspace, device drivers, or successful boot path has been demonstrated for XT2135-2. XNU source alone is not a complete iOS installation; proprietary Apple components and extensive hardware/platform integration would also be involved. Do not redistribute proprietary Apple software, firmware, keys, or assets.
