# Architecture Overview

This document describes the layers that would need investigation. It does not claim that these layers currently work on the Moto G60.

## Conceptual layers

1. **Device firmware and boot chain** — device-specific firmware, bootloader policy, image verification, and the documented route for loading an operating-system kernel.
2. **Kernel handoff** — the interface by which a boot environment supplies memory, hardware descriptions, and other platform information to a kernel.
3. **Kernel and platform support** — CPU and interrupt handling, memory management, timers, buses, and platform-specific services.
4. **Device drivers** — storage, display, input, networking, audio, sensors, power management, and other peripherals.
5. **Operating-system user space** — system services, libraries, frameworks, applications, and system management.
6. **Platform integration and security** — boot trust, code signing, sandboxing, entitlements, updates, and device-specific policy.

## XNU is not the whole operating system

XNU is a kernel. Public XNU source does not provide the complete proprietary iOS user space, frameworks, device-specific drivers, firmware, signing infrastructure, or all platform integration required for an iPhone-class operating system.

Therefore, a hypothetical kernel boot would be only one small milestone. It would not demonstrate that iOS 26 is running.

## Project architecture decision

The current research direction is to investigate the existing Motorola boot environment and whether a carefully scoped kernel handoff experiment is theoretically possible. This is an investigation only; compatibility with XNU is not established.

## Questions that must be answered

- What exact boot interfaces does the target firmware expose?
- What platform information is passed to a kernel?
- Which required XNU platform components are absent?
- Can the required drivers and user-space components legally and technically be obtained?
- Can the original device state be recovered if an experiment fails?

Until these questions have evidence-based answers, no implementation architecture should be treated as validated.
