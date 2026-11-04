# Hardware Support Inventory

The table below is a provisional research inventory. It is not a statement that any component is supported by XNU or by this project.

| Item | Current project note | Status |
|---|---|---|
| Device | Motorola Moto G60 | Target; exact variant must be confirmed |
| Codename | `hanoip` | Reported; verify against device-specific sources |
| SoC | Qualcomm Snapdragon 732G | Reported; verify exact board |
| CPU architecture | ARM64 | Expected from the reported platform; confirm |
| GPU | Adreno 618 | Reported platform specification; no project support |
| Display | 1080 × 2460 class | Verify exact panel/variant |
| Memory | Multiple configurations reported | Confirm the user's exact variant |

## Subsystem support matrix

| Subsystem | Evidence of project support | Notes |
|---|---|---|
| CPU and exception handling | None | Platform-specific work unknown |
| Memory management | None | Requires platform integration |
| Interrupt controller and timers | None | Unknown |
| Storage | None | Driver and boot integration unknown |
| Display and GPU | None | No graphics support established |
| Touch input | None | Unknown |
| USB and charging | None | Unknown |
| Wi-Fi and Bluetooth | None | Firmware and driver availability unknown |
| Cellular modem | None | Complex platform integration |
| Audio | None | Unknown |
| Cameras | None | Unknown |
| Sensors | None | Unknown |
| Power management | None | Unknown |

## Evidence requirements

For every new entry, record the exact model, board revision, firmware, source URL, evidence label, and any limitations. Do not infer support merely because another device uses a related SoC.
