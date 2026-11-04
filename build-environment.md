# Build Environment

## Current scope

The current phase is host-side research and documentation. This repository does not yet define a validated build system, toolchain, kernel configuration, or bootable image.

## Suggested research workstation practices

- Use a supported, up-to-date operating system on the development computer.
- Keep project source and notes under version control.
- Record compiler and tool versions when later experiments become justified.
- Verify source provenance and licenses before building or importing code.
- Keep backups of research notes and any original, legally obtained device documentation.

## Not yet specified

The project has not selected or validated:
- a cross-compilation toolchain;
- an XNU configuration for the Moto G60;
- a platform-specific linker or boot configuration;
- device drivers;
- an image packaging format;
- a safe device test procedure.

These should not be guessed. They depend on the results of the boot-chain and platform feasibility research.

## Safety boundary

Do not build or flash an experimental image based solely on generic ARM64 instructions or instructions for a different phone. The exact board, boot interface, and recovery method must be established first.
