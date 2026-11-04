# Roadmap

This roadmap is a research plan, not a promise that every milestone is achievable.

## M0 — Documentation and project setup
- [x] Define the target and project principles.
- [x] Document the distinction between XNU and a complete iOS system.
- [ ] Choose an appropriate license for original project materials.
- [ ] Add source references for all device-specific claims.

## M1 — Device and source research
- [ ] Confirm the exact Moto G60 model variants and board identifiers.
- [ ] Collect authoritative bootloader, firmware, kernel, and device-tree references.
- [ ] Identify the relevant public XNU source version and its platform assumptions.
- [ ] Record which required components are unavailable or proprietary.

## M2 — Boot-chain feasibility
- [ ] Document the device's verified-boot and bootloader model from reliable sources.
- [ ] Understand supported image formats and documented boot interfaces.
- [ ] Assess whether a research-only handoff prototype is even plausible.
- [ ] Define a recovery and rollback plan before considering device-side experiments.

**Gate:** Do not modify or flash the phone during this phase.

## M3 — Kernel and platform compatibility
- [ ] Compare XNU's supported architectures and platform dependencies with the target.
- [ ] Inventory required low-level platform services.
- [ ] Identify the gap between generic ARM64 support and this specific SoC/board.
- [ ] Decide whether a minimal kernel feasibility prototype is realistic.

## M4 — Hardware support assessment
- [ ] Display and graphics
- [ ] Touch input
- [ ] Storage and filesystem
- [ ] USB and charging
- [ ] Audio
- [ ] Wi-Fi and Bluetooth
- [ ] Cellular modem and telephony
- [ ] Sensors, cameras, and power management

## M5 — iOS 26 system compatibility assessment
- [ ] Identify required user-space and framework dependencies.
- [ ] Document platform security and signing requirements at a high level.
- [ ] Assess the availability and licensing of required components.
- [ ] Distinguish a kernel experiment from a functioning iOS system.

## M6 — Prototype decision
- [ ] Publish an evidence-based go/no-go assessment.
- [ ] If viable, define a narrowly scoped, non-destructive prototype.
- [ ] If not viable, document the blockers and stop rather than make unsupported claims.

## M7 — Validation
Only pursue this milestone if earlier gates are satisfied and a safe, recoverable test plan exists.
- [ ] Define reproducible tests.
- [ ] Record exact device variant and firmware.
- [ ] Publish results, limitations, and known failures.

## Current restriction

No experimental image should be flashed to the Moto G60 as part of the current documentation and research phase.
