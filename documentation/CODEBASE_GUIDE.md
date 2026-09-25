# Codebase Guide

This guide describes the directory structure and the core
principles of the codebase.

## Directory Structure

-   `include/`: All public and internal headers.
    -   `uapi/`: Headers shared with userspace (IOCTL definitions).
    -   `kernel/`: Internal kernel-only headers.
-   `src/`: Primary source code directory.
    -   `kernel/`: Linux kernel module source (C).
    -   `gpu/`: GPU kernels (CUDA, HIP, or OpenCL).
    -   `lib/`: Userspace library for interacting with the subsystem.
-   `tests/`: Test suites.
    -   `unit/`: Small-scale functional tests.
    -   `integration/`: Kernel-to-GPU integration tests.
    -   `benchmarks/`: Performance measuring scripts and applications.
-   `tools/`: Helper scripts for loading modules, debugging, and
    building.
-   `scripts/`: Automation for CI/CD and system configuration.

## Coding Standards

1.  **Kernel Code**: Follow the Linux Kernel Coding Style (tabs,
    80-char limit, descriptive naming).
2.  **GPU Code**: Use clear naming for global/device functions;
    separate host-side launch code from device-side kernels.
3.  **Error Handling**: Use standard Linux error codes (e.g.,
    `-ENOMEM`, `-EINVAL`) for kernel functions and IOCTL returns.
4.  **Synchronization**: Always document locking mechanisms
    (mutexes, spinlocks) used to protect shared data between CPU
    and GPU tasks.

## Build System

-   **CMake**: Used for building userspace components and tests.
-   **Kbuild**: Used for building the kernel module.
-   A top-level `Makefile` or script should orchestrate both build
    systems.
