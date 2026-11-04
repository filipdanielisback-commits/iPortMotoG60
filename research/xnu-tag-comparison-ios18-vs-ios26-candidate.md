# XNU tag comparison: iOS 18-era and iOS 26-era candidate

**Research date:** 2026-11-04  
**Scope:** Static source comparison only. No device access, builds, flashing, bootloader changes, or installation.

## 1. Revisions compared

| Comparison label | Apple XNU tag | Interpretation |
|---|---|---|
| iOS 18-era reference | [xnu-11215.1.10](https://github.com/apple-oss-distributions/xnu/tree/xnu-11215.1.10) | The tag exists in Apple's public XNU repository. Its association with an iOS 18-era/Darwin 24.0 release is reported by secondary version research, not an Apple tag-to-iOS mapping. |
| iOS 26-era candidate | [xnu-12377.1.9](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9) | The tag exists in Apple's public XNU repository. Secondary kernel-version research associates it with iOS 26.0 / Darwin 25.0. Apple's public distribution metadata inspected for this project did not provide a direct XNU mapping. |

Do not treat either label as a complete release compatibility statement. In particular, `xnu-12377.1.9` is a candidate source revision for this comparison, not an Apple-confirmed universal iOS 26 source pin.

## 2. Repository comparison result

GitHub's compare endpoint for [xnu-11215.1.10...xnu-12377.1.9](https://github.com/apple-oss-distributions/xnu/compare/xnu-11215.1.10...xnu-12377.1.9) reported:

- The newer tag is ahead by 2 commits.
- 300 files are listed as changed across the comparison.
- The largest changed areas are BSD networking and BSD kernel code.
- No changed paths were reported in the inspected ARM startup, ARM64 startup, ARM platform-expert, or IOKit directories.

The 300-file count describes the Git comparison between these two tags; it does not mean that 300 platform drivers were added or that hardware support expanded for non-Apple devices.

## 3. Startup and platform files checked

The following paths were selected because they are part of the generic ARM64 startup and platform initialization path:

| Source path | Role in the source tree | Comparison result |
|---|---|---|
| `osfmk/arm/arm_init.c` | Early ARM kernel initialization; calls platform initialization | Not listed as changed |
| `osfmk/arm64/start.s` | ARM64 reset/startup assembly and early CPU setup | Not listed as changed |
| `pexpert/arm/pe_init.c` | ARM platform-expert initialization | Not listed as changed |
| `iokit/Kernel/IOStartIOKit.cpp` | Initializes the IOKit root platform nub and service matching | Not listed as changed |

This is a path-level comparison result, not a proof that every runtime behavior is identical. It does indicate that this particular tag transition did not introduce visible edits to these four core files.

## 4. What this means for Moto G60 XT2135-2

The device research in this repository identifies the handset as the Motorola Moto G60 XT2135-2, in the Hanoip device family. Motorola's published kernel source for the supplied Android build is Linux 4.14.190, not XNU.

The comparison does **not** reveal Hanoip support being added to XNU:

- No Hanoip-specific platform expert has been identified in the inspected XNU paths.
- No matching Qualcomm/Hanoip peripheral driver set has been demonstrated in the inspected XNU source.
- Generic ARM64 startup code is not a substitute for board-specific boot integration, interrupt-controller support, clocks, power management, storage, display, touch, audio, camera, modem, Wi-Fi, and other device support.
- A kernel source tag alone does not provide the proprietary iOS userspace, frameworks, services, firmware, or signing and boot infrastructure needed for a complete iOS system.

**Conclusion:** These two XNU snapshots provide useful research references, but the comparison supplies no evidence that either one can boot on the Moto G60. Genuine iOS 26 operation on XT2135-2 remains unimplemented and un demonstrated in this project.

## 5. Sources

### Primary source
- [Apple's public XNU repository](https://github.com/apple-oss-distributions/xnu)
- [XNU tag xnu-11215.1.10](https://github.com/apple-oss-distributions/xnu/tree/xnu-11215.1.10)
- [XNU tag xnu-12377.1.9](https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9)
- [GitHub tag comparison](https://github.com/apple-oss-distributions/xnu/compare/xnu-11215.1.10...xnu-12377.1.9)

### Secondary version references
- [The Apple Wiki: XNU version history](https://theapplewiki.com/wiki/XNU) — secondary reference for Darwin/XNU build strings; not an Apple release manifest.
- [NewOSXBook source browser: xnu-12377.1.9 ARM initialization](https://www.newosxbook.com/src.php?file=%2Fosfmk%2Farm%2Farm_init.c&tree=xnu) — secondary source browser for a tagged source snapshot.

### Project device evidence
- [XT2135-2 device profile](../docs/device-profile-xt2135-2.md)
- [Hardware inventory and XNU gap analysis](./hardware-inventory-xnu-gap-analysis.md)
- [XNU source notes](../third_party/xnu/README.md)

## 6. Next research milestone

The next useful computer-only task is to audit XNU's public ARM64 machine/platform configurations and IOKit driver inventory against the Hanoip hardware inventory. Record each device component as **matching source found**, **no matching public source found**, or **not yet investigated**. Do not infer compatibility from a generic ARM64 target or a Qualcomm-related source filename.
