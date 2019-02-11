# MicroHypervisor
Arrow normally runs on Hypervisor at Cloud and Edge segments. Since Arrow is desgined to run the single task. The Hypervisor should be very small amd safe, and also can be configurable according to the task.
Currently the Arrow technology is developed on Qemu which is not so small, but it is very stable and a very good Hypervsor for developing.
At same time the cutting edge Micro Hypervisor technologies are also being investigated by us, which are list below.
"[Arrow Service](https://github.com/Walnux/arrowd)" is designed to support different Hypervisors through crossbow engines. 

## the Nemu(None emulation Hypervisror)
It is the efforts in Qemu community to make qemu more small and quick by removing the feature simuation, and old unnecessary devices.

## AWS Firecracker
Here’s what you need to know about Firecracker:

- Secure – This is always our top priority! Firecracker uses multiple levels of isolation and protection, and exposes a minimal attack surface.

- High Performance – You can launch a microVM in as little as 125 ms today (and even faster in 2019), making it ideal for many types of workloads, including those that are transient or short-lived.

- Battle-Tested – Firecracker has been battled-tested and is already powering multiple high-volume AWS services including AWS Lambda and AWS Fargate.

- Low Overhead – Firecracker consumes about 5 MiB of memory per microVM. You can run thousands of secure VMs with widely varying vCPU and memory configurations on the same instance.

- Open Source – Firecracker is an active open source project. We are already ready to review and accept pull requests, and look forward to collaborating with contributors from all over the world.

- Firecracker was built in a minimalist fashion. We started with crosvm and set up a minimal device model in order to reduce overhead and to enable secure multi-tenancy. Firecracker is written in Rust, a modern programming language that guarantees thread safety and prevents many types of buffer overrun errors that can lead to security vulnerabilities.

- Firecracker Security
As I mentioned earlier, Firecracker incorporates a host of security features! Here’s a partial list:

- Simple Guest Model – Firecracker guests are presented with a very simple virtualized device model in order to minimize the attack surface: a network device, a block I/O device, a Programmable Interval Timer, the KVM clock, a serial console, and a partial keyboard (just enough to allow the VM to be reset).

- Process Jail – The Firecracker process is jailed using cgroups and seccomp BPF, and has access to a small, tightly controlled list of system calls.

- Static Linking – The firecracker process is statically linked, and can be launched from a jailer to ensure that the host environment is as safe and clean as possible.

## rust-vmm
https://github.com/rust-vmm/community
