# Apple XNU upstream source

**Status:** Official upstream XNU source located; iOS 18 and iOS 26-era source tags checked. No Hanoip port exists yet.

## Official upstream repository

- Repository: https://github.com/apple-oss-distributions/xnu
- Owner: Apple OSS Distributions
- Apple describes XNU as the kernel used by Darwin-based operating systems, including macOS and iOS.
- The upstream README documents ARM64 support and explains that `pexpert` contains platform-specific code. ARM64 support alone does not establish support for the Moto G60 / Hanoip.

## Version research: iOS 18 and iOS 26

The tags below were checked by fetching the `README.md` file from Apple's official XNU repository at each tag. This verifies that the tags exist in the official repository. The iOS release association is a separate claim and is labelled according to the available evidence.

| Target family | XNU tag | Evidence and confidence |
|---|---|---|
| iOS 18.0 era | `xnu-11215.1.10` | Official Apple XNU tag exists. A secondary kernel-version reference maps this version family to iOS 18.0 / Darwin 24.0. Treat as a strong version-family match, not proof that this exact tag matches every iOS 18 point release or device. |
| iOS 26 era | `xnu-12377.1.9` | Official Apple XNU tag exists. A third-party technical research page associates it with iOS 26.4.1 / Darwin 25. This is a useful candidate, but the association has not been independently confirmed from an Apple-published XNU-to-iOS mapping. |

Direct official source links:

- iOS 18-era tag: https://github.com/apple-oss-distributions/xnu/tree/xnu-11215.1.10
- iOS 26-era tag: https://github.com/apple-oss-distributions/xnu/tree/xnu-12377.1.9
- Official XNU repository: https://github.com/apple-oss-distributions/xnu

Additional version-mapping references (secondary sources, not Apple):

- iOS 18 / Darwin 24 kernel version history: https://theapplewiki.com/wiki/XNU
- iOS 26.4.1 research citing XNU `xnu-12377.1.9`: https://github.com/cloverfield11/ios26-hypervisor-research

Apple's public iOS distribution metadata currently identifies iOS 26.0, but the inspected `release.json` lists WebKit and libiconv tags, not an XNU tag. Therefore it does not itself establish the XNU revision for iOS 26:
https://github.com/apple-oss-distributions/distribution-iOS/blob/main/release.json

## Important interpretation

Do not call either tag “the complete iOS source.” XNU is the kernel, not the complete iOS operating system. The public XNU repository does not by itself provide the full iOS user space, proprietary frameworks and services, device-specific firmware, signing materials, or complete platform integration.

Do not describe an arbitrary checkout of the moving `main` branch as “the iOS 26 kernel.” For reproducible work, pin a specific tag or commit and record the evidence linking it to the target OS build.

## Relationship to iPortMotoG60

The target device is Motorola Moto G60 XT2135-2 (Hanoip), with the user-reported Android 12 build `S2RIS32.32-20-9-9-2-3`.

The Motorola source investigated by this project identifies a Linux 4.14.190 kernel. That is useful hardware and boot-process reference material, but it is not an XNU port.

The generic ARM64 support in XNU does not demonstrate that either tag can boot on Hanoip. A real port would still require platform initialization and working support for the board's interrupt controller, timers, memory map, storage, display, input, power management, and other required devices. Necessary proprietary or undocumented components may also be unavailable.

## How upstream source is handled here

This file is a source pointer, not a copy of Apple's code. The XNU source remains maintained by Apple in its upstream repository.

If a local source checkout is added later:
1. Record the exact upstream tag and commit SHA.
2. Preserve upstream license files and notices.
3. Keep upstream source separate from project-authored Hanoip changes.
4. Document the evidence linking the source revision to the claimed Apple OS release.
5. Never add leaked, proprietary, or privately obtained Apple files.

A Git submodule can be considered when a local checkout is needed. It should pin a reviewed commit rather than silently track a moving branch.

## Current result

- [x] Official Apple XNU repository identified.
- [x] Official XNU tag `xnu-11215.1.10` checked (iOS 18-era candidate).
- [x] Official XNU tag `xnu-12377.1.9` checked (iOS 26-era candidate).
- [x] Difference between an XNU kernel and the complete iOS system documented.
- [ ] Exact XNU revision matched to a specific iOS 26 device/build using Apple-published evidence.
- [ ] Hanoip-specific XNU platform support implemented.
- [ ] Hanoip drivers and boot integration implemented.
- [ ] XNU boot on the Moto G60 demonstrated.

**No device changes or boot experiments are part of this research update.**
