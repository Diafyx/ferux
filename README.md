# Ferux

A general-purpose operating system written in Rust, engineered for safety and correctness.

[![License: Apache-2.0](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](LICENSE)

> **Status: pre-alpha.** Ferux does not boot yet. There is no release, and nothing here is ready for real use.

## Overview

Ferux is an operating system for developers, for secure systems, and for everyone else.

Ferux is written in Rust. Rust checks memory safety at compile time, but an operating system still has to do things the compiler cannot check, such as talking to hardware and managing page tables. In Rust, that code is marked `unsafe`.

Ferux's core design rules are about that code:

- **All `unsafe` code lives in one trusted core crate.** Every other part of Ferux, however large it grows, is safe Rust that the compiler checks.
- **Every `unsafe` block states why it is sound**, in a `// SAFETY:` comment.
- **The trusted core is measured.** CI will track how much `unsafe` code exists, so it can only grow with a reason.
- **Proofs over time.** The parts of the trusted core that matter most, such as page tables and memory allocation, are candidates for formal verification.

Only the trusted core is kept small, because a smaller trusted core is easier to review and prove correct.

## Roadmap

| Version | Goal |
|---|---|
| 0.1.0 | Boots on x86-64 in QEMU through Limine (UEFI), writes to the serial port and the screen, reports panics, and CI boots and tests it on every pull request |
| 0.2.0 | CPU setup and interrupts: every CPU exception is caught and reported, safe handling of stack overflows, timer and keyboard |
| 0.3.0 | Memory: physical memory management, page tables and a kernel heap |
| 0.4.0 | Multitasking: kernel threads, a scheduler and safe locking |
| 0.5.0 | User mode: programs in user mode, system calls and ELF program loading |
| 0.6.0 | Files and shell: a file system layer, a RAM disk and a first shell |

The current milestone and its issues are on the [milestones page](https://github.com/Diafyx/ferux/milestones). Each version is planned in detail when work reaches it.

## Getting started

There is nothing to build yet. Build and run instructions arrive with the Rust workspace and the build runner in milestone 0.1.0.

## Contributing

Issues and pull requests are welcome. Please read the [contributing guide](CONTRIBUTING.md) first, and open an issue before starting anything larger than a small fix. Every change goes through an issue and a reviewed pull request, and every commit must be signed and signed off.

Everyone taking part in Ferux is expected to follow the [code of conduct](CODE_OF_CONDUCT.md).

## Security

To report a security vulnerability, follow the [security policy](SECURITY.md). Please do not open a public issue.

## License

Ferux is licensed under the [Apache License, Version 2.0](LICENSE). See [NOTICE](NOTICE).
