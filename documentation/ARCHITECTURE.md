# Architecture Overview

This document describes the high-level architecture of the
GPU-accelerated kernel subsystem.

## System Diagram

```mermaid
graph TD
    subgraph Userspace
        App[Application]
        Lib[Subsystem Library]
    end

    subgraph "Kernel Space (Host CPU)"
        KMod[Kernel Module Driver]
        KMem[Kernel Memory Management]
        Scheduler[Workload Scheduler]
    end

    subgraph "GPU Hardware / Driver"
        GPUDriver[GPU Vendor Driver]
        GPU[GPU Hardware]
    end

    App --> Lib
    Lib --> KMod
    KMod --> GPUDriver
    GPUDriver --> GPU
    KMod <--> KMem
    KMod <--> Scheduler
```

## Component Descriptions

1.  **Kernel Module Driver**: The core entry point for the
    subsystem. Handles IOCTLs and system calls from userspace.
2.  **Workload Scheduler**: Manages the offloading of specific
    kernel tasks (e.g., encryption, compression) to the GPU.
3.  **Memory Manager**: Handles Zero-Copy or DMA transfers between
    CPU kernel memory and GPU memory.
4.  **GPU Kernels**: The actual logic (CUDA/OpenCL/HIP) running on
    the hardware.

## Data Flow

1.  Kernel intercepts a high-throughput task.
2.  Scheduler evaluates GPU availability.
3.  Memory Manager maps kernel buffers to GPU-accessible space.
4.  GPU executes the kernel.
5.  Results are synchronized back to the CPU kernel context.
