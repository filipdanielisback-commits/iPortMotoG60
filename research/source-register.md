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

## Evidence labels

- **Primary:** manufacturer documentation or source code published by the manufacturer.
- **Community:** public device trees, recovery trees, or community kernel projects.
- **Owner-reported:** information supplied by the project owner from device settings.
- **Inferred:** a cautious conclusion drawn from multiple sources.
- **Unknown:** not established by available evidence.

Every new research note should include the source URL, date checked, exact model/variant, and evidence label.
