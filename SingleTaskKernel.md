# Standard Linux Kernel based Single Task Kernel
## What is Arrow Single Task Kernel

Single task kernel is based on starndard Linux Kernel which is optimized and tailored for a single applicaiton to run. The single application can be any applications running on linux Operating System. The only 2 limitations for the application are:

* It must be staticly linked. For the kernel only runs a single application, there is no reason to keep the complication of the Dyanmically Linked Library. Staticly linked application only includes the code the application really needs. Basing on the asumption that only statically linked application supported. A [lot of innovations](/TechnologyBlueprint.md) can be work out to make Arrow simple, safe, fast and small basing on the standard Linux kernel.   

* Could not start up another application

The reason to use Linux kernel is for the production purpose. Since Linux Kernel has been battle-tested. We don't want to reinvent the wheels like what are doing in many unikernel projects. Besides, we believe that Standard Linux has the potential to be optimized to be small and quick enough for the single task purpose and provides the standard Linux application running environment for the vast amount of applications running on Cloud. [Arrow 0.1 release](/Release01.md) has proved it.

## How far we will go to optimize Linux Kernel for Single Task
[Some research are ongoing to change Linux Kernel into a unikernel LibOS](https://www.researchgate.net/publication/332329656_Unikernels_The_Next_Stage_of_Linux's_Dominance)
[Some projects even started](https://next.redhat.com/2018/11/14/ukl-a-unikernel-based-on-linux/)

### Single Task Kernel supports Multi-process
A lot of applications are actually is multipul process architecture. The good example is Nginx.  

### Keep ring transition
Although ring transition bring some overhead, but it seperate the user application which running the unpriviligy area from the kernel spaces which running the priviligy code. It does provide the foundmental security protection for user applications. see [Unikernels are unfit for production](https://www.joyent.com/blog/unikernels-are-unfit-for-production).

For the purpose of production, our princeple is Security first. 

### avoid any potential License issue
Linux Kernel code is licesed under GPLV2. If changing Linux Kernel into unikernel style Libraries and link them with the application. The applicaition will be contaminated. That means that the application may have to be released under GPLV2. It is impossible for most of the applications.

For the purpose of production, we must avoid any potential legal issues.

In Single Task Linux, Kernel actually does not link with applicaiton. Instead, application binary is loaded to user space areare and run on top of Kernel just same as application run on standard Linux OS.  

## Single Task optimizaiton on Linux kernel

### optimization on application loader

## Unikernel and Single Task Kernel
Unikernel is a libOS 


Single Task Kernel retains all the advantages of Linux like the battle tested code base, hudge open source community and vast supporting of legacy software
