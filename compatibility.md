# Compatibility Assessment

## Current status

<badge>Not demonstrated</badge>

There is currently no verified evidence in this repository that XNU or iOS 26 boots on the Motorola Moto G60 (`hanoip`).

## Compatibility matrix

| Area | Assessment | Evidence |
|---|---|---|
| ARM64 instruction set | Potential architectural overlap only | Does not establish platform support |
| Moto G60 bootloader handoff | Unknown for an XNU kernel | Device-specific research required |
| XNU platform support for this board | Not established | No validated port |
| Required peripheral drivers | Not established | No project drivers |
| Complete iOS 26 user space | Not available in this project | XNU source is not complete iOS |
| Apple platform security integration | Not established | Significant unresolved requirements |
| Overall iOS 26 compatibility | Unproven | No working port demonstrated |

## Why a related device is not proof

A different phone using a related processor may have a different board design, boot chain, memory layout, display, peripheral configuration, firmware, and driver set. Results from another device cannot be treated as a drop-in solution for the Moto G60.

## Evidence standard

A claim of successful boot must identify the exact device variant and firmware, describe what actually booted, provide reproducible evidence, and clearly distinguish a kernel test from a complete operating system. A screenshot or interface mock-up alone is not sufficient evidence that iOS is running.
