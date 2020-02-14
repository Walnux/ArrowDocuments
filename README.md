# What is Arrow?
**Arrow is a simple, secure, low latency and low overhead way to run applications on cloud, edge Computing and native computer environment.**

Arrow is based on the [**Application Central**](/TopDown.md) design philosophy.

[**Arrow System**](/ArrowSystemVision.md) is the end to end solution to develop, debug, release, deploy and run Arrows.


# Arrow overview
[People are waiting for a simple, secure, low latency and low overhead way to run applicaion in cloud.](ArrowIsUseful.md)

In oder to achieve the goal, Arrow is desgined and implemented using Application Central philosophy.

## Arrow is Application Central Solution
[Application centrialized philosophy](TopDown.md#application-central-philosophy) starts from the application. Only the components that are needed by the specific applicaiton is inlcuded. All the other components which is not used by the application should be removed.

- Arrow only runs the single staticly linked application which only includes the libaries binaries the application really needs. NO Dynamical Linked Libraries(DLL) are packaged with the application.
- This application is directly combined with the tailored single task kernel. The rootfs which normally contains shell, tools, and system services is removed. Logially, the kernel is part of the application.
- The single task kernel is based on the standard Linux Kernel, which provides the standard Linux running environment for an application to run. The applicaiton still runs in userspace and call Kernel through standard system call machanism. The ring transition is kept. The Application does not need any porting work. So abundant of mature applications can run as Arrow without any modification.
- Since the Kernel is refined for the purpose of single task for cloud usage. Except for the legacy devices drivers and uncesssary features, the block devices, all the filesystems components and even the application loader to run applications are all removed from the kernel. So the single task kernel can be very slim and fast. [See Arrow Application Loader](/Benefits.md)
- Lightweight Virutal Machine which is based on Kernel Virtural Machine(KVM) is refined to be tailored for the single task cloud usage. It can also be very small and fast. Virtual Machine is used as the sandbox to run the single applicaiton.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowFramework.png">
</p>

- Arrow Service configures the network environment for bounch of Arrow applictions connecting with each other through standard TCP/IP network. So Arrow is the typical Application Central solution which can avoid [the problems caused by System Central solution](TopDown.md#problems-caused-by-system-central-solution).   
- Arrow is simple to use. [Arrow System](/ArrowSystemVision.md) - the end to end solution to run an Arrow on cloud is designed for users to run an Arrow easily and intuitively.
- Arrows are naturally suitable for Microservice. They can be orchestrated to work together to fullfill the specific goal with Kubernates in cloud environment. Arrow also can be integrated into users' FaaS solutions.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowSystem.png">
</p>

## Arrow Perfomance Goal
- **Memory overhead goal for each Arrow Instance:  < ~(1-2)M**
With [Application Centrialized Top Down](/path/to/topdown) design philosophy, and [lightweight Virtual Machine](/path/to/lightweithtVirtualMachine) technology for moden cloud and edge computing usages, several [foundmental innovations](/path/to/innovations) are worked out for Arrow to [run application with very small overhead](/path/to/overhead). 

- **Arrow application loading latency goal: approaching native application loading**
Arrow itself is very small and can be preinstalled so the loading latency is small, further more, the [Arrow template and clone technology](/path/to/AtemplateClone) technology and [Arrow application sharing](/path/toAshareing) technology makes Arrow application loading latency approach native application loading.



# Current statues and plan
## [Arrow 0.1 release](/path/to/0.1Release)

Arrow 0.1 is released to prove the Arrow concept. Some mainstream applications are proved to work properly as Arrow.

- Busybox, Python, NodeJs, Kubernetes(Golang), Redis*, Nginx can run as Arrow. 
- ASDK(Arrow System Development Kit) which is based on Alpine to build Arrow(attached mode) images
- Linux kernel with Aloader, Ainit, Anotify features added to implement the Single task kernel
- Qemu-KVM based virtural machine is used
- Arrow service for running and managing Arrows. Arrow Life-cycle, Network, Anotify, Crossbow, Engine, Qemu-engine, log, I/O, Arrow Spec features are provided from the Service

## [post 0.1 design & plan](/Path/to/0.2ReleasePlan): Focus on Virtualization Technology
Arrow is based on lightweigh virtualizaion technology. After 0.1 release,  Arrow work will focus on rust-vmm based lightweight vmm.   

- Rust-VMM based Lightweight VMM technolgy
- Virtro-App
- memory plugin
- vmm clone & template
- ShadowFS
- Vsock based Network
- Adebug: Coredump file
- Run more applications as Arrow

## The goal of the Arrow Project: Ready for Open Source

# Getting Started
## How to run Arrow project
Firstly, you can start from [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK).
