# What is Arrow project?
## The goal of Arrow Project
**Arrow project intends to explore a simple, secure, low latency and low overhead way to run mordern software-as-a-service(SaaS) applications on cloud, edge or client computing environment.**

Arrow is based on the [**Application Central**](/TopDown.md) design philosophy and [Twelve-Factor App methodology](https://12factor.net/).

## The motivation to work on Arrow project
Currently, if you want to run applications on a specific computing system, you have to install (or package) them into some kind of Operating System(OS), and then run the OS in the client computing environemnt or deploy the OS together with your applications on cloud or edge infrastrucure through Virtual Machine Images or Contianer Images.

This method brings users the compatiblity with the old systems but It also inherits all the problems from them.

In order to run the specific applications, users have to spend quit a few efforts to manage and maintain the OS which is much more complicated than the application itself in most situations. Furthermore they have to endure the potential system vulnerability caused by the complication. Besides, the System itself normally is much bigger than the applicaitons users want to run. That is one of the main reasons why computing system becoming bigger and slower. And in cloud and edge computing epic, with huge number of applicaitons are moved to cloud and edge computing, the problem becomes severe.

Ironically, people are trying to use more complicated technologies to resolve the problems which are caused by the complicaiton itself. More and more new technolgies are introduced into computing system and try to make it faster and safer. 

We are trying to find a fundamentaly simple way to run applications and make computing system safe and fast whether on Cloud, Edge or client side. It is our motivation to work on Arrrow project.

Then what is the fundamentaly simple way to run an applicaiton?

## Just run the applicaiton
Could we just run the application and don't have to care about the OS and infrastructure detail? To achieve it, Arrow uses [Application Central Solution](TopDown.md#application-central-philosophy). This solution focuses on the Applicaiton itself not system.

**Arrow** 
- Runs a single staticly linked application. NO Dynamical Linked Libraries(DLL) are packaged with the application.
- Runs the application directly on the single task kernel. Rootfs Image containing shell, tools, and system services and libraries is eleminated.
- Runs the application in the standard Linux environment provided by the single task kernel based on upstream Linux kernel. That means the applicaiton still runs in userspace and call Kernel through standard system call machanism and the ring transition is kept.
- Runs the application without any porting work. So abundant of mature applications can run without any modification.
- Runs the application as well as Single Task Kernel on Kernel Virtural Machine(KVM) based lightweight Virutal Machine(VM). 
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowFramework.png">
</p>

An application running with the single task kernel on the lightweight VM can be called as an **Arrow Instance**.  

- Connecting several Arrow Instances with standard TCP/IP based network, thses Instances can be combined and scaled up to any type of Cloud services.
- Arrow Instances can also be easily integrated and managed by mainstream orchstration system like K8S.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowInstances.jpg">
</p> 

## Arrow system might change cloud and edge
With Arrow system, users don't have to package everything (OS, third party services and middleware) into their owner Container or VM images which will be deployed onto a specific cloud infrastructrue to run. Instead, the standard mainstream third party applications can be standardized as Arrow Instances and invoked by user to connect with the user applications and serve as the service from cloud and edge computing. Obviously, Arrow is designed to support Microservice architecutre. This method also can greatly simplify and unify the cloud, edge infrastructure and client computing. Please refer [Arrow System project](TopDown.md#application-central-philosophy) for detail

We believe Arrow will change cloud edge and client computing.

## Make Arrow small and fast
at first glance, running single application with single task kernel on VM might cause a lot overhead and latency. However, We believe with moden lightweight Hypervisor technologies and other innvations in Single Task kernel as well as Arrow Services we can make Arrow Instance very small and fast.

The performance goal for Arrow Instance is set as below: 

- **Memory overhead goal for each Arrow Instance:  < ~(1-2)M**
With [Application Centrialized Top Down](/path/to/topdown) design philosophy, and [lightweight Virtual Machine](/path/to/lightweithtVirtualMachine) technology for moden cloud and edge computing usages, several [foundmental innovations](/path/to/innovations) are worked out for Arrow to [run application with very small overhead](/path/to/overhead). 

- **Arrow application loading latency goal: approaching native application loading**
Arrow itself is very small and can be preinstalled so the loading latency is small, further more, the [Arrow template and clone technology](/path/to/AtemplateClone) technology and [Arrow application sharing](/path/toAshareing) technology makes Arrow application loading latency approach native application loading.

##  Getting Started
- You can start from building some mainstream projects with [Arrow Service Development Kit (ASDK)](https://github.com/Walnux/Atools/tree/master/ASDK).

- Then, the Attached Mode Arrow Images can be used to run as Arrow instance through [Arrow Service](https://github.com/Walnux/arrowd)

- [Run Busybox as Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/ArrowizeBusybox.md)

- [Run Nginx as Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nginx.md)

- [Run Nodejs Apps as Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nodejs.md)

## Related Projects

Arrow project is consist of several sub projects.
- Single Task Kernel
- Arrow Service
- ASDK
- Lightweight-Hypervisor

## Current statues
## [Arrow 0.1 release](/path/to/0.1Release)

Arrow 0.1 was released to prove the basic Arrow concept by running some popular mainstream applications as Arrow Instances.

- Busybox, Python, NodeJs, Kubernetes Master services(Golang), Redis, Nginx can run as Arrow Instances. 
- ASDK can be used to build the Attached Mode Arrow images.
- Aloader, Ainit, Anotify components are added into Linux kernel to implement the Single Task Kernel.
- Qemu-KVM based virtural machine is used.
- Arrow service prototype was worked out to manage Arrow Instances Life-cycle, Network, logging and I/O etc.

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
