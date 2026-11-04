# Apple XNU upstream source

**Status:** Upstream source identified; not yet integrated or ported to Hanoip.

## Official source

- Repository: https://github.com/apple-oss-distributions/xnu
- Owner: Apple OSS Distributions
- Project description: XNU is the kernel used by Darwin-based operating systems, including macOS and iOS.
- Architecture note: The upstream project documents ARM64 support. ARM64 support alone does not establish support for the Moto G60 / Hanoip platform.

## iOS 26 versioning caveat

Do not describe an arbitrary checkout of the upstream `main` branch as “the iOS 26 kernel.” XNU is published as source snapshots, and a source tree's exact relationship to a particular iOS release must be established from its version metadata and matching Apple release information.

This project has not independently verified a source snapshot as the exact XNU revision shipped by iOS 26. Until that evidence is recorded, use the wording **“Apple's public XNU source (revision not yet matched to iOS 26)”**.

The public XNU repository is not a complete iOS 26 source release. It does not by itself provide the full iOS user space, proprietary frameworks and services, device-specific firmware, signing materials, or the complete platform integration required to run iOS.

## Relationship to iPortMotoG60

The target device is Motorola Moto G60 XT2135-2 (Hanoip), with the user-reported Android 12 build `S2RIS32.32-20-9-9-2-3`.

The Motorola source investigated by this project identifies a Linux 4.14.190 kernel. That is useful hardware and boot-process reference material, but it is not an XNU port.

The XNU source's generic ARM64 support does not demonstrate that it can boot on Hanoip. A real port would still require, at minimum, platform initialization and working support for the board's interrupt controller, timers, memory map, storage, display, input, power management, and other required devices. The necessary proprietary or undocumented components may also be unavailable.

## How the upstream source is handled here

This file is a source pointer, not a copy of Apple's code. The XNU source remains maintained by Apple in its upstream repository.

A future source checkout should:
1. Record the exact upstream commit SHA or verified release tag.
2. Preserve the upstream license and notices.
3. Keep upstream source separate from project-authored Hanoip changes.
4. Document the exact source revision and the evidence linking it to any claimed Apple OS release.
5. Never add leaked, proprietary, or privately obtained Apple files.

A Git submodule can be considered when a local checkout is needed. It should pin a specific reviewed commit rather than silently track a moving branch.

## Current result

- [x] Official Apple XNU repository identified.
- [x] Upstream ARM64 support noted.
- [x] Distinction between XNU and the complete iOS system documented.
- [ ] Exact iOS 26 XNU revision verified.
- [ ] Hanoip-specific XNU platform support implemented.
- [ ] Hanoip drivers and boot integration implemented.
- [ ] XNU boot on the Moto G60 demonstrated.

**No device changes or boot experiments are part of this research update.**
