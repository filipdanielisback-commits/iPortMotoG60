# Boot Process Research

## Purpose

Record the questions that must be answered before considering any experimental kernel handoff on the Moto G60.

## Research checklist

- Confirm the exact model and board variant.
- Identify the bootloader and firmware versions relevant to that variant.
- Find authoritative documentation for the device's boot sequence.
- Determine which image formats and boot interfaces are officially or demonstrably supported.
- Understand verified-boot policy and the role of image signatures.
- Identify the recovery and restore process using trusted, device-specific documentation.
- Record whether a proposed experiment can be evaluated without writing to device storage.

## Non-destructive-first principle

The initial work should be performed on a computer using source code, documentation, and static analysis. A temporary boot mechanism, if one exists for the device, must not be assumed to accept an arbitrary kernel or an XNU-compatible image. Its existence does not prove that XNU can use the handoff environment.

## Required evidence before any device test

A future proposal must include:
- exact device variant and firmware;
- authoritative description of the boot interface;
- a clear explanation of what the test changes and what it does not change;
- a verified recovery path;
- a way to stop safely if assumptions fail.

No device flashing or partition modification is part of the current project phase.
