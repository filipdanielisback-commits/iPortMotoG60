# XNU feasibility checklist — XT2135-2

**Phase:** research only  
**Target:** Moto G60 XT2135-2  
**Goal:** determine whether a genuine XNU-based research prototype is technically plausible. This checklist does not authorize device modification.

## Gate 1 — Exact device and firmware identity

- [ ] Record the Android build number from Settings > About phone.
- [ ] Record the software channel/region if displayed.
- [ ] Record the Android version and security patch date.
- [ ] Match the exact firmware build to a manufacturer-published source package.
- [ ] Distinguish XT2135-2-specific evidence from generic hanoip-family evidence.

## Gate 2 — Public source completeness

- [ ] Identify the exact matching kernel source revision.
- [ ] Identify the device tree and board configuration for the exact variant.
- [ ] Determine whether required boot firmware and device-specific components are documented.
- [ ] Record source licenses and keep proprietary components out of the repository.

## Gate 3 — Platform architecture research

- [ ] Document CPU architecture and supported execution levels from reliable sources.
- [ ] Document memory map and interrupt-controller requirements from public technical documentation.
- [ ] Identify the display, storage, USB, power, and timer interfaces at a high level.
- [ ] Map which required interfaces have public specifications and which remain undocumented.
- [ ] Separate generic ARM64 XNU support from handset-specific driver support.

## Gate 4 — Boot-chain feasibility (documentation only)

- [ ] Find authoritative documentation for the XT2135-2 boot chain.
- [ ] Determine the documented image/container formats at a conceptual level.
- [ ] Identify verified-boot constraints and recovery provisions from trusted sources.
- [ ] Establish whether a supported, non-destructive test mechanism is documented.
- [ ] Do not infer that a generic Android fastboot feature is supported by this phone.

## Gate 5 — iOS 26 scope

- [ ] Separate open-source XNU components from proprietary iOS components.
- [ ] List required platform services and frameworks that are not supplied by XNU.
- [ ] Identify the licensing and redistribution boundaries.
- [ ] Define a realistic research milestone that does not claim to deliver complete iOS 26.

## Stop conditions

Stop and return to research if any critical fact is unknown, if a proposed test could damage the only handset, or if recovery cannot be independently established. No flashing, partition changes, bootloader changes, or experimental boot images are part of the current phase.

## Current conclusion

**Feasibility: undetermined and high-risk.** Public Android source is useful for understanding the device, but it does not establish an XNU port or a working iOS 26 boot path.
