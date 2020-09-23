
## The goal of Arrow Project
**Arrow project targets to explore a simple, secure, low latency and low overhead way to run [micoservices](https://martinfowler.com/articles/microservices.html) based applications on cloud, edge, client even IoT computing platform and obey [Twelve-Factor App methodology](https://12factor.net/).**

## The motivation to work on Arrow project
It is well-known, how to run applications decided nearly every aspect of cloud and edge computing including infrastructure, applications development, operation, security and so on. 

Traditional Virtual Machine Image-based way to run application trigged the booming of one of the main cloud service ECS (Elastic Computing Service). It provides the similar user experience and compatible application running environment with the physical server. Multi-tent user applications running on the virtual server are well isolated and protected. However, although users don’t have to manage the physical server anymore, maintaining and operating the full feature virtual machine-based virtual server is still a heavy burden. 

Kubernetes and Container technology-based Cloud Native is the trending of modern cloud computing. The applications are packaged into Container image which is orchestrated by Kubernetes. User doesn’t have to touch the server anymore, which is called serverless. It is a revolution in cloud computing technology. Running applications in container is being widely adopted by people as the standard cloud native way to run applications. But container technology still comes with some issues. 

First, applications running in containers share the same host kernel. So multi-tent applications are not well isolated. The stability and security might be a potential risk especial in commercial public cloud computing and multi-tend edge computing environment. In order to resolve the stability and security issue, normally the extra sandbox technology like Virtual Machine or [gvisor](https://gvisor.dev/) technology have to be used to isolate each tenant’s containers running environment from the host system. Obviously, this increases system complication, sacrifices the performance, impacts the high-density, flexibility and many other benefits from Container technology. 

Second, although not necessary, in order to acquire the full compatible running environment, most of the traditional applications are still packeted with the base operation system as well as the DDL(Dynamical Link Library), runtime and other OS components to run, which increases the image size, impacts the application startup latency, wastes the system storage resource and network bandwidth. The base OS, DDL, and other OS components might also incur some potential security risks and increases the operating and maintaining burden. Ironically, many of the components of the OS actually never be used by the application. The problem might become worse in edge computing and IoT area where system resources are limited while security, and latency is critical, operation difficulty is higher than that in cloud environment.   

Third, The Container runtime framework is not simple, packaging, configure and run the container image is not always very easy. The union-FS system is useful for sharing the contents among Container images, but this filesystem is heavy and slow. And the sharing of the contents is not efficient. In order to share the contents, the layers containing the same content among different images must obey exact the same layer order.  

Forth, although running single process in container is encouraged, the compatibility with the native OS environment is one of the most favorite features the Container technology provides. It allows (or indulges) people to package the heavy full feature OS with bunch of applications. The expense is that the infrastructure has to take the burden to handle these heavy working-loads. that increases the system complication and can’t make full use of the benefits from the modern innovations of Cloud Native technology where the microservice based applications are adopted as the main cloud service framework. 

So, all in all, Cloud Native needs a new way to run applications where Container technology and traditional Virtual Machine technology can’t handle very well. 

It is the motivation to kick off the Arrow project. 

## Arrow philosophy

It is not necessary for Arrow to support all the applications and cover all the usage cases. Arrow project targets to run microservices architecture applications on cloud, edge even client and IoT environment which obey [Twelve-Factor App methodology](https://12factor.net/).   

In order to achieve the goal, below questions have to be asked: 

- Can users just run an application (or microservice) on cloud (or edge) as simply as possible and don’t have to care about packaging their own software with OS, runtime, middleware or other applications into some kind of image? 

- Can each application (or microservice) run in an isolated, secured, relatively compatible environment and don’t need to be ported and big change? 

- Can applications (or microservices) easily be deployed, run and operated on the distributed cloud, edge infrastructure or even on the client or IoT environment? 

- Most importantly, can the applications (or microservices) running latency be kept as low as possible, running overhead be kept as small as possible? 

## Single Task Concept 

Compared with the monolithic application, microservices architecture application is composed of the independent microservices cooperated with each other with TCP/IP based communication method and service APIs. 

Each independent microservice is a single application which is called task in Arrow project. In order to answer above questions. Arrow combines the single task with the single task kernel and runs them on the light weight virtual machine. 

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowFramework.png">
</p>

Only running the single application, the DDL is not necessary any more, the application is statically linked, and doesn’t have to be packaged with the base OS and other components. So, the microservice working-load can be very small and simple. 

Running the single task, the standard Linux kernel is simplified and redefined to run the single application, and the standard Linux application running environment like Kernel user space ABI and FHS compatibility are protected. So, application don’t have to be modified to run. 

Obviously, it is the best isolated and security way to run each microservice. 

In order to make sure the microservices can run seamlessly on Cloud Native environment, and easily be deployed and run on the distributed cloud or edge infrastructure. Arrow project must keep compatible with Kubernetes. 

The challenge task for Arrow project is to decrease the latency and overhead. With the single task concept in mind, a lot of innovations can be done in the single task kernel and Pod Hypervisor which creates and manages the single task virtual machine in the pod and talk with Kublet/Kubernetes). The microservice running latency and overhead can be greatly decreased. See detailed in single task kernel project and Pod hypervisor project.  

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowInstances.jpg">
</p> 

Arrow is the exploration and innovation project. Welcome to join this amazing adventure!  

## Getting Started
- You can start from [Arrow Service Development Kit (ASDK)](https://github.com/Walnux/Atools/tree/master/ASDK).

- Then run Arrow Instances below through [Arrow Service](https://github.com/Walnux/arrowd)

- [Run Busybox Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/ArrowizeBusybox.md)

- [Run Nginx Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nginx.md)

- [Run Nodejs Applications Arrow Instances](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nodejs.md)

- [Run Python Applications Arrow Instances](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/python.md)

- [Run Golang Applications Arrow Instances](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/golang.md)

## Arrow sub-projects
- Single Task Kernel
- Arrow Service
- Pod Hypervisor
- [Arrow Service Development Kit (ASDK)](https://github.com/Walnux/Atools/tree/master/ASDK)


## Arrow 0.1 Release

[Arrow 0.1 release](/path/to/0.1Release)

Arrow 0.1 was released to prove the basic Arrow concept by running some popular mainstream applications as Arrow Instances.

- Busybox, Python, NodeJs, Kubernetes Master services(Golang), Redis, Nginx can run as Arrow Instances. 
- ASDK can be used to build the Attached Mode Arrow images.
- Aloader, Ainit, Anotify components are added into Linux kernel to implement the Single Task Kernel.
- Qemu-KVM based virtural machine is used.
- Arrow service prototype was worked out to manage Arrow Instances Life-cycle, Network, logging and I/O etc.

## Arrow 0.2 Release

[Arrow 0.2 release plan](/Path/to/0.2ReleasePlan): Focus on Virtualization Technology
Arrow is based on lightweigh virtualizaion technology. After 0.1 release,  Arrow work will focus on rust-vmm based lightweight vmm.   

- Rust-VMM based Lightweight VMM technolgy
- Virtro-App
- memory plugin
- vmm clone & template
- ShadowFS
- Vsock based Network
- Adebug: Coredump file
- Run more applications as Arrow
