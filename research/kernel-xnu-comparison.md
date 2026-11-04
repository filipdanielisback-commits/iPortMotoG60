# Kernel source and XNU comparison — XT2135-2

**Research date:** 2026-11-04  
**Device:** Moto G60 XT2135-2  
**Reported software:** Android 12, build `S2RIS32.32-20-9-9-2-3`  
**Scope:** Source-code inspection only; no device interaction or modification

## 1. Exact Motorola kernel release located

Motorola's kernel source issue #574 names the exact firmware package:

`XT2135-2_HANOIP_RETEU_12_S2RIS32.32-20-9-9-2-3_subsidy-DEFAULT_regulatory-XT2135-2-EUROPE_CFC.xml.zip`

A Motorola contributor closed the issue after publishing the source release:

- Issue: https://github.com/MotorolaMobilityLLC/kernel-msm/issues/574
- Matching release tag: https://github.com/MotorolaMobilityLLC/kernel-msm/releases/tag/MMI-S2RIS32.32-20-9-9-2-3
- Repository: https://github.com/MotorolaMobilityLLC/kernel-msm

The release tag is an exact build-string match to the owner's reported build. This is strong evidence that a matching Motorola Linux kernel source release exists.

## 2. Kernel source inspected

The release's root `Makefile` reports:

- Linux kernel version **4.14.190**.
- This is Linux kernel source, not XNU.
- The inspected root Makefile declares GPL-2.0 licensing.

The release's Qualcomm device-tree Makefile contains a `CONFIG_HANOIP_DTB` section and lists Hanoip EVT1, DVT1, and DVT2 overlay targets. The corresponding overlay files declare:

- `model = "hanoip"`
- Qualcomm MSM ID value `365`
- Board IDs `0x4C 0xA100`, `0x4C 0xB100`, and `0x4C 0xB200` for the three inspected overlay variants.

These are source-level identifiers. The existence of several board overlays means we must not guess which board revision is in the owner's handset from the Android build string alone.

The common Hanoip overlay includes shared descriptions for:
- Motorola/Qualcomm platform configuration
- Audio
- Fingerprint
- Panel/display
- Battery and thermal configuration
- Sensors
- Touchscreen
- NFC over an I2C interface
- UFS-related configuration

This demonstrates that the Android kernel source contains substantial board-specific hardware description. It does not by itself prove that every referenced component is present in the exact handset configuration, nor does it provide an XNU driver.

## 3. XNU source inspected

Apple's public XNU repository:

https://github.com/apple-oss-distributions/xnu

Its README describes XNU as the Darwin kernel, with Mach, BSD components, and IOKit. It states that XNU supports ARM64 as an architecture.

Important distinction:

**ARM64 architecture support is not the same as support for this Motorola board.**

A device-specific port still needs platform initialization and working drivers for the exact SoC and peripherals. The public XNU source tree includes platform-specific areas such as `pexpert` and the IOKit driver framework, but the existence of these frameworks does not supply Hanoip/Qualcomm device drivers.

## 4. Preliminary compatibility assessment

| Area | Evidence found | Assessment |
|---|---|---|
| CPU instruction-set family | Motorola Android kernel source has ARM64 architecture support | Promising at architecture level only |
| Board identity | Hanoip device-tree overlays and board IDs exist | More variant identification needed |
| Interrupts, clocks, GPIO and power | Device-tree descriptions and platform includes exist | Must map required services to XNU support |
| Display and touch | Panel and touchscreen includes are referenced | No matching XNU drivers demonstrated |
| Storage | UFS configuration is referenced | No matching XNU storage driver demonstrated |
| Audio, camera, sensors, NFC | Device-tree includes and peripheral descriptions exist | No complete XNU driver set demonstrated |
| Boot handoff | No validated XNU boot path established | Unknown; do not experiment |
| iOS 26 userland | Not supplied by XNU source | Separate, major unresolved requirement |

## 5. What this means

The exact Motorola Linux source is now identified and selected source files have been inspected. This is a real research milestone.

However, the source is a Linux 4.14.190 Android kernel tree. It is not an XNU port and cannot simply be relabelled or substituted for XNU. Device-tree data can help document hardware, but Linux drivers are not directly usable as XNU drivers without substantial engineering and compatible interfaces.

No successful XNU boot, iOS 26 userspace, or working Hanoip XNU driver set has been demonstrated.

## 6. Next research tasks

1. Inventory the exact Hanoip device-tree files included by the release.
2. Identify the precise board overlay used by the XT2135-2 firmware, without guessing from the model name.
3. Map the main hardware blocks to public documentation and XNU platform interfaces.
4. Review XNU's ARM64 platform code at a conceptual/source level and document missing board support.
5. Record unresolved boot-chain and recovery questions without attempting a boot test.

## Safety boundary

All work remains on a computer and uses public source code and documentation. Do not flash, unlock, repartition, replace boot images, or test experimental boot paths on the handset.
