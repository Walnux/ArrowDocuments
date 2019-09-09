# What is Arrow?
**Arrow is the way to run the application on cloud.**

The application is combined with the tailored single task kernel and run on the lightweight Virtual Machine.

Arrow is based on the [**Application Centrialized Top Down**](/path/to/topdown) design philosophy.

Except for cloud, Application can aslo run as Arrow on edge computing and native computer.

Arrow can run application safely, simply and swiftly.

**Arrow System** is the end to end solution to run and manage Arrows.


# Arrow overview

Arrow provides a safe way to run application by Combining it with the tailored single task kernel and running it on the Virtual Machinn. All the unnecessary components like Dynamical Link Libearis, Shell, tools, even the rootfs, the kernel block devices, the related filesystem components and even the application loader to run applications and so on are all removed. And the safe lightweight Virtual Machine is used.

Arrow is the safe way to run application because:
- Arrow runs single applicaton isloated in the sandbox.
- By removing all the unnecessary components, the attack interface is reduced greatly.
- Even an Arrow is hacked, it is very difficult to be manipulated to attack or hack others, since Arrow can only run sigle applicaton one time, and the resources can be used to hack are very limited.
- the save lightweigh VirtualMachine can also protect the security

Arrow is quite easy and intuitive to use. Unlike packaging, shipping software in some workload and run the workload on cloud. With Arrow you just run the applicaton. Arrows are designed to for Microservice. They can be orchestrated to work together to fullfill the specific goal with Kubernates in cloud environment. Arrow also can be integrated into users' FaaS solutions.

The single task kernel is based on Linux kernel. And the application runs in the standard Linux environment. So all the applications running on Linux can run as Arrow with [very few limitations](/path/to/limitation). Abundant Linux applications can run as Arrow with help of [ASDK Arrow System Development Kit](/path/to/ASDK).

Swift means small, fast and flexible.

- **Memory overhead goal for each Arrow:  < ~(1-2)M**
With [Application Centrialized Top Down](/path/to/topdown) design philosophy, and [lightweight Virtual Machine](/path/to/lightweithtVirtualMachine) technology for moden cloud and edge computing usages, several [foundmental innovations](/path/to/innovations) are worked out for Arrow to [run application with very small overhead](/path/to/overhead). 

- **Arrow is very small**
Arrow is the applicaton combined with single task kernel running on lightweight Virtual Machine, as mentioned above, it only contain the necessary binary segments which can be preinstalled or intalled ondemand and shared by all the users. At most situations the Virtual Machine with the single task kernel can also be shared by all the users. Besides, Arrow is desinged seperated from data and configuration. the only thing needs to ship is the configurations as well as the stateful data used to setup the environemnt or mirgration of the stateful applications.

- **Arrow application loading latency goal: approaching native application loading**
Arrow itself is very small and can be preinstalled so the loading latency is small, further more, the [Arrow template and clone technology](/path/to/AtemplateClone) technology and [Arrow application sharing](/path/toAshareing) technology makes Arrow application loading latency approach native application loading.

- **Arrow is single application and quite flexible and easy to be orchestrated and shared** 
 Compared with the heavy full OS stack Virtual Machine or Container workload, Arrow is quite flexible to be managed and orchestrated and shared. Since it focus running single application. It is natively suitable for microservice architecture. And most important is that the single application can be shared and composed by all the users flexiblely. So users do not need to include the same applications in their individual workload.

# Current statues and plan
## [Arrow 0.1 release](/path/to/0.1Release): prove of Concept
-Busybox, Python, Node, Kubernetes(Golang), Redis*, Nginx are proved to be running as Arrow 
-ASDK(Arrow System Development Kit) whcih is based on Alpine to build Arrow(attached mode) images
-Linux kernel with Aloader, Ainit, Anotify features added to implement the Single task kernel
-Qemu-KVM based virtural machine is used
-Arrow service for running and managing Arrows. Arrow Life-cycle, Network, Anotify, Crossbow, Engine, Qemu-engine, log, I/O, Arrow Spec features are provided from the Service

## [Arrow 0.2 design & plan](/Path/to/0.2ReleasePlan): Make arrow useful
- Run more applications as Arrow
- Arrow template, Arrow Clone, Arrow Share 
- Lightweight VM
- ShadowFS
- AutoBalloon
- Optimization on Singl task kernel
- Adebug

## [Arrow 0.3 Goal]: Make it product


# Users are waiting for a safe simple and swift way to run applicaion in cloud
Currently, the main workload in cloud is traditional full feature Virtual Machine with the full feature guest OS, middlewares and libraris to run applications. It is very redundant and slow. And the overall infrastrucure is also quite complicated. 

Recent years, Container like Docker comes to dominate the cloud workload. Containers can be used to package, ship and run the software isolated directly on the hostOS. Containers share the same kernel which greatly increases the code running indensity and efficiency. But container is not sandbox. Security and stability is a problem. Besides Container like docker container implementaion is very complicated . And not easy to be used at some resource limtted edge computing environemnt or some FaaS solution directly like AWS Greengrass. Furthermore, although Docker Container can be used to package single application, most people still tend to use it to package the whole system ever running on the virtual Machine. That is one of the reason why docker container suceed. But it can't help the whole cloud and edge ecosystem small and simple.

Arrow shares some basic views with Unikernel like run single application on Virutal Machine. But Arrow is actually differnt solution with Unikernel. Unikernel is the libOS which link application with the specific OS libearis and run on VM. While Arrow makes use of existing mature Linux Kernel. And Application runs on the standarnd Linux environment. So Arrow can make full use of exising Linux resources. Most importantly most of these resources are well verified and safe enough for Arrow to reach the production quality.

However, Arrow can't do everything. It can't be used to package the whole OS system. Arrow System can be think of part of hostOS or cloud infrastrucre to package and run sigle application. With Arrow System, users do not need to package and ship their own software, instead they only need to ask Arrow System to run some specific applications as Arrows to compose and fullfill their specific goal.     
