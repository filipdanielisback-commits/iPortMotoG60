# Project Status — iPortMotoG60

**Last updated:** 2026-11-04  
**Target:** Motorola Moto G60 XT2135-2  
**Reported software:** Android 12, build `S2RIS32.32-20-9-9-2-3`

> **Status terminology:** “Working” means completed and supported by repository evidence. “Not working” means not implemented or not demonstrated yet; it does **not** mean the phone was tested and failed. “In development” means active computer-only research. No experimental boot, flashing, partition changes or device modification has been performed.

## Working

- [x] GitHub repository created and connected to the intended account.
- [x] Target model and reported Android build recorded.
- [x] Matching Motorola kernel-source release tag identified: `MMI-S2RIS32.32-20-9-9-2-3`.
- [x] Matching source root Makefile inspected; it identifies Linux kernel **4.14.190**.
- [x] Hanoip device-tree overlays located for EVT1, DVT1 and DVT2 board IDs.
- [x] Selected display, touchscreen, audio, sensor, camera, NFC and battery/thermal device-tree descriptions inspected.
- [x] XNU public source inspected for ARM64 initialization, platform-expert startup and IOKit initialization.
- [x] Preliminary Linux-hardware-to-XNU gap analysis documented.
- [x] Source register updated with primary source links.
- [x] Work kept computer-only and non-destructive.

**Evidence / documents**
- [Device profile](../docs/device-profile-xt2135-2.md)
- [Kernel and XNU comparison](kernel-xnu-comparison.md)
- [Hardware inventory and XNU gap analysis](hardware-inventory-xnu-gap-analysis.md)
- [Source register](source-register.md)

## Not working / not demonstrated

These are **not currently available project capabilities**. Most have not been tested on the phone.

- [ ] Booting XNU on the Moto G60 XT2135-2 — not demonstrated.
- [ ] A working Hanoip-specific XNU platform expert / board bring-up — not implemented.
- [ ] Working XNU drivers for this board's display, touchscreen, GPU, audio, cameras, storage, NFC, fingerprint, sensors, modem, Wi-Fi or Bluetooth — not demonstrated.
- [ ] Confirmed board-revision identification for the owner's exact handset — unknown.
- [ ] A verified and supported boot-chain handoff from Motorola's bootloader to XNU — unknown.
- [ ] A complete Darwin/iOS-compatible userspace and required Apple frameworks/services — not implemented.
- [ ] A genuine iOS 26 system running on this phone — not demonstrated.

The existence of ARM64 support in XNU does not establish compatibility with this Qualcomm/Motorola board. The public Linux source is hardware documentation and is not a ready-made XNU port.

## In development

- [ ] **Phase 3 — Platform research:** map the base device tree, CPU/SoC startup assumptions, memory map, interrupt controller, timers and clocks.
- [ ] Determine which Hanoip board overlay applies to XT2135-2 using reliable documentation, without changing the phone.
- [ ] Trace Linux driver source paths for the major peripherals and record their hardware interfaces.
- [ ] Compare each required subsystem with public XNU platform and IOKit interfaces.
- [ ] Identify public documentation/specifications needed for any possible independent driver implementation.
- [ ] Maintain a feasibility and recovery-risk assessment before considering any device-side work.

## Next milestone

Produce a source-backed **platform bring-up requirements document** covering early ARM64 startup, memory, interrupts, timers, clocks, GPIO and storage. Keep this milestone strictly read-only; do not flash, unlock, repartition or boot experimental images.

## Safety and scope

This repository currently tracks research, not a working port. Do not treat a source-code match or a device-tree description as proof that a component works under XNU. Do not add proprietary Apple system files, firmware, signing keys, leaked materials or personal device identifiers.
