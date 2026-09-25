# Project Tasks (TODO)

## Phase 1: Foundation & Setup
- [ ] Initialize repository structure (`src/`, `include/`, `tests/`)
- [ ] Set up build system (CMake + Kbuild for kernel module)
- [ ] Create a "Hello World" kernel module (loading/unloading)
- [ ] Implement basic IOCTL interface for userspace testing

## Phase 2: GPU Integration (Research & POC)
- [ ] Select primary GPU target (NVIDIA CUDA or AMD ROCm)
- [ ] Implement a basic GPU kernel (e.g., vector addition)
- [ ] Research DMA/GDRCopy (GPU Direct RDMA) from the CPU kernel
- [ ] Create a proof-of-concept for offloading a single task from
    kernel space

## Phase 3: Subsystem Development
- [ ] Design the `k-gpu-scheduler` for managing concurrent requests
- [ ] Implement memory pooling for kernel-GPU buffers
- [ ] Add support for multiple GPU devices (discovery and load
    balancing)

## Phase 4: Testing & Optimization
- [ ] Performance benchmarking (CPU vs GPU vs Hybrid)
- [ ] Stress test for memory leaks in the kernel context
- [ ] Implement comprehensive unit tests for the userspace library
- [ ] Security audit (memory safety between kernel and GPU)
