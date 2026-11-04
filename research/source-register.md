# Source register

This register separates primary documentation from community-maintained Android configuration. A source describing the related `hanoip` family is not automatically proof about every XT2135-2 firmware variant.

## Device identity and installed build

| Source | What it supports | Limitations |
|---|---|---|
| Motorola conformity documentation: https://en-emea.support.motorola.com/app/answers/detail/a_id/160550/~/regulatory-information | Motorola model/regulatory identity listings, including XT2135-2 | Regulatory listing is not a full hardware or boot-chain specification |
| Owner-reported device settings (2026-11-04) | Android 12 and build `S2RIS32.32-20-9-9-2-3` on the target handset | User-provided device information; not independently queried from the handset |

## Motorola kernel sources

| Source | What it supports | Limitations |
|---|---|---|
| https://github.com/MotorolaMobilityLLC/kernel-msm | Motorola's public kernel-source organization | Repository organization alone does not identify the matching source revision |
| https://github.com/MotorolaMobilityLLC/kernel-msm/issues/574 | Release reference naming XT2135-2 firmware `S2RIS32.32-20-9-9-2-3` and a corresponding firmware/source package | A release reference is not independent verification that the source was downloaded, inspected, built, or matches every component on the handset |

Exact package name referenced in the Motorola issue:
`XT2135-2_HANOIP_RETEU_12_S2RIS32.32-20-9-9-2-3_subsidy-DEFAULT_regulatory-XT2135-2-EUROPE_CFC.xml.zip`

The package naming suggests the RETEU / Europe channel. Treat this as a lead to verify against the handset's software channel and the source release contents, not as a confirmed regional identity.

## Android device configuration

| Source | What it supports | Limitations |
|---|---|---|
| https://github.com/motorola-sm6150-devs/device_motorola_hanoip | Community Android device tree for the hanoip family | Not proof of Motorola support for XNU; family-level rather than guaranteed variant-specific |
| https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/BoardConfig.mk | Android build values such as ARM64 target, board platform label, boot image configuration | Values are Android build settings, not a bootloader compatibility guarantee |
| https://github.com/motorola-sm6150-devs/kernel_motorola_sm6150 | Community Android kernel source repository | Linux kernel source, not an XNU port |


## Exact XT2135-2 kernel source inspection (2026-11-04)

| Source | What was inspected | Findings and limits |
|---|---|---|
| https://github.com/MotorolaMobilityLLC/kernel-msm/releases/tag/MMI-S2RIS32.32-20-9-9-2-3 | Release tag matching the owner's exact build | Release is linked by Motorola contributor from issue #574; tag title describes a Hanoip Android 12 push |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/Makefile | Root kernel Makefile at matching tag | Identifies Linux 4.14.190; this is Linux, not XNU |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/Makefile | Qualcomm device-tree build list | Contains Hanoip DTB/DTBO build entries for EVT1, DVT1 and DVT2 variants |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-evt1-overlay.dts | Hanoip EVT1 overlay | Declares model `hanoip`, MSM ID 365, board ID 0x4C/0xA100 |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-dvt1-overlay.dts | Hanoip DVT1 overlay | Declares model `hanoip`, MSM ID 365, board ID 0x4C/0xB100 |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-dvt2-overlay.dts | Hanoip DVT2 overlay | Declares model `hanoip`, MSM ID 365, board ID 0x4C/0xB200 |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-common-overlay.dtsi | Shared Hanoip device-tree overlay | References panel, audio, fingerprint, battery/thermal, sensor, touchscreen and NFC configuration; does not itself prove exact fitted components or supply XNU drivers |
| https://github.com/apple-oss-distributions/xnu/blob/main/README.md | Apple's public XNU README | Describes XNU and states ARM64 architecture support; architecture support is not board-specific Hanoip support |

Detailed findings and limitations: [kernel/XNU comparison](kernel-xnu-comparison.md).


## Hardware inventory and XNU comparison (2026-11-04)

Detailed inventory and gap analysis: [hardware-inventory-xnu-gap-analysis.md](hardware-inventory-xnu-gap-analysis.md).

| Source | Inspected evidence | Limitation |
|---|---|---|
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-evt1-overlay.dts | Hanoip EVT1 overlay, MSM ID 365, board ID 0x4C/0xA100 | Does not prove this is the board revision in the owner's handset |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-dvt1-overlay.dts | Hanoip DVT1 overlay, board ID 0x4C/0xB100 | Same variant-identification limitation |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-dvt2-overlay.dts | Hanoip DVT2 overlay, board ID 0x4C/0xB200 | Same variant-identification limitation |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/hanoi-panel.dtsi | Tianma ILI7807S 678 / 1080×2460 DSI panel description | Source configuration, not live panel identification |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoi-touchscreen.dtsi | Ilitek SPI touchscreen node | No XNU driver identified |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-audio-overlay.dtsi | WCD9375 sound-card configuration | No XNU audio stack identified |
| https://github.com/MotorolaMobilityLLC/kernel-msm/blob/MMI-S2RIS32.32-20-9-9-2-3/arch/arm64/boot/dts/qcom/sdmmagpie-hanoip-sensor-overlay.dtsi | Semtech SX933x sensor node | Exact fitted sensor not independently confirmed |
| https://github.com/apple-oss-distributions/xnu/blob/main/pexpert/arm/pe_init.c | ARM platform-expert initialization and device-tree-to-IOKit startup | Generic platform infrastructure, not Hanoip support |
| https://github.com/apple-oss-distributions/xnu/blob/main/osfmk/arm/arm_init.c | ARM/ARM64 initialization and platform setup flow | Generic kernel initialization, not proof of board compatibility |
| https://github.com/apple-oss-distributions/xnu/blob/main/iokit/Kernel/IOStartIOKit.cpp | IOKit root nub initialization from device-tree pointer | Generic IOKit startup, not device drivers |

## Evidence labels

- **Primary:** manufacturer documentation or source code published by the manufacturer.
- **Community:** public device trees, recovery trees, or community kernel projects.
- **Owner-reported:** information supplied by the project owner from device settings.
- **Inferred:** a cautious conclusion drawn from multiple sources.
- **Unknown:** not established by available evidence.

Every new research note should include the source URL, date checked, exact model/variant, and evidence label.
