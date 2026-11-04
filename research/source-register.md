# Source register

This register separates primary documentation from community-maintained Android configuration. A source describing the related `hanoip` family is not automatically proof about every XT2135-2 firmware variant.

## Device identity

| Source | What it supports | Limitations |
|---|---|---|
| Motorola conformity documentation: https://en-emea.support.motorola.com/app/answers/detail/a_id/160550/~/regulatory-information | Motorola model/regulatory identity listings, including XT2135-2 | Regulatory listing is not a full hardware or boot-chain specification |
| Motorola support documentation: https://en-emea.support.motorola.com/ | Manufacturer documentation entry point | Confirm the exact guide revision and region before relying on details |

## Android device configuration

| Source | What it supports | Limitations |
|---|---|---|
| https://github.com/motorola-sm6150-devs/device_motorola_hanoip | Community Android device tree for the hanoip family | Not proof of Motorola support for XNU; family-level rather than guaranteed variant-specific |
| https://github.com/motorola-sm6150-devs/device_motorola_hanoip/blob/lineage-20/BoardConfig.mk | Android build values such as ARM64 target, board platform label, boot image configuration | Values are Android build settings, not a bootloader compatibility guarantee |
| https://github.com/motorola-sm6150-devs/kernel_motorola_sm6150 | Community Android kernel source repository | Linux kernel source, not an XNU port |

## Motorola kernel sources

- Motorola source organization: https://github.com/MotorolaMobilityLLC
- Search for the exact XT2135-2 firmware build before selecting a kernel source revision.
- Do not assume a repository with a similar chipset or codename matches the installed firmware.

## Evidence labels

- **Primary:** manufacturer documentation or source code published by the manufacturer.
- **Community:** public device trees, recovery trees, or community kernel projects.
- **Inferred:** a cautious conclusion drawn from multiple sources.
- **Unknown:** not established by available evidence.

Every new research note should include the source URL, date checked, exact model/variant, and evidence label.
