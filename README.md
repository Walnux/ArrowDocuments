# What is Arrow?
**Arrow is the application.**

The application is combined with the tailored single task kernel running on the lightweight Virtual Machine.

With Arrow you can run the application on cloud, edge computing and native computer safely, simply and swiftly.

**Arrow services** is a set of tools to run and manage Arrows


# Arrow Overview
Arrow is the application [which can be run](/path/to/example) as simply as a normal application natively. Arrows are designed to for Microservice. They can be orchestrated to work together to fullfill the specific goal with K8S in cloud environment. Arrow also can be integrated into customer's FaaS solutions.

The single application is combined with the tailored single task kernel running on the Virtual Machine. So the application actually runs isolately in the sandbox. Besides, single application directly combine with kernel and all the uncessary components like Dynamical Libearis, Shell, rootfs, block devices based filesystem components and application loader to run applications and so on are all removed and only single application can run onetime in the single task kernel. So Application can run as Arrow very safely. 

The single task kernel is based on Linux kernel. And the application runs in the stardard Linux environment. In theory the all the applications running on Linux can run as Arrow with [very few limitations](/path/to/limitation). So the abundant Linux applications can run as Arrow with [ASDK Arrow System Development Kit](/path/to/ASDK).

Swift means small, fast and flexible.

With [application centralized top down design phylosophy](/path/to/topdownPhylosophy) and [moden lightweight Virtual Machine technology](/path/to/lightweithtVirtualMachine), [Foundmental innovations](/path/to/innovations) are worked out for Arrow to [run application with very small overhead](/path/to/overhead). 

- Arrow can reach < ~1M/applicaion memory overhead
- Arrow application loading latency can approach native application  

Arrow is the applicaton which is seperated from data and configuration. Arrow only needs to contain the necessary binary segments which can be preinstalled or intalled ondemand and shared by different users. Since each Arrow runs in its isloated environemnts, the only thing needs to ship is the configurations as well as the stateful data used to setup the environemnt or mirgration of the stateful applications. So Arrow could be very small fast and flxible. 

# Why Arrow is useful?
All in all, Arrow is the safe, simple and swift way to to run application on cloud, edge computing and native environemnt. 

Traditional standard full feature Virtual Machine running the full feature guest OS with middlewares and libraris to run application is basing on [OS centrialized bottom up philosophy](/path/to/bottomUp). It is very redundant and slow.

Container can be used to package and run the software directly on hostOS with CGroup and technoloies to isolate

Arrow share some basicl views with Unikernel like run single application on Virutal Machine. But Arrow is actually differnt solution with Unikernel. Unikernel is the libOS which link application with the specific OS libearis and run on VM. While Arrow makes use of existing mature Linux Kernel. And Application runs on the standarnd Linux environment. So Arrow can make full use of exising Linux resources. And most important most of these resources are well verified and mature and safe enough. So Compared with Unikernel, Arrow is easy to reach production quality. 

However, there already have several avaible workloads. Why Arrow is needed?



Swift means small and fast. Arrow seperates application from data and configuration from begining. 

Other than Virtual Machine and Container technology, Arrow provides another Safe, Simple, Swift, Small Agnostic and Compatible  way to develop, package, release, deploy, run, manage and orchestate tasks in cloud, edge, native, even embedded environemnt.

Arrow technology is application centralized. Unlike running an Operating System on Virtual Machine, or running tasks in Container, Arrow itself is the task the applicaton or the service. With [Arrow service)](/path/to/Arrow_Infrastructure), user can run Arrow as easy as running a normal application.

What different is that all the Arrowized applications are runing in "fully" isolated environemnt. They can be connected with each other through TCP/IP based Arrow Network. Since Arrow infrastructure is desgined from begining to be compatible with Container(like Docker container) and container orchestartion system like Kubernetes. Arrow can be easily integrated into Kubernetes and seamless cooperate with the existing Container infrastructure.

Arrow provides a very safe way to run user application, since each application combine and runs on its own tailed single task kernel which exactly matches the requiremnts of the application. At same time the single task kernel runs on the highly configured Hypervisor like Qemu-KVM or Nemu-KVM.[See Arrow Design Philosophy](/path/to/Arrow_Philosophy) The combination of static linked application with tailed kernel greatly increase the security by reducing the number of attacking interfaces. The single task kernel running on Hypervisor provides throughly isolation for each application. Obviously, with Arrow technology, users can run their tasks safely and stably. 

Arrow is small and fast. With the innovative technoloies like:

- "[Application Loader & single task Kernel](/path/to/Arrow_Application_Loader_Single_Task_Kernel)", 
- "[Kernel Sharing](/path/to/Arrow_Kernel_Sharing)",
- "[In-memory Filesystem](/path/to/Arrow_In_memory_Filesystem)",
- "[Micro Hypervisor](https://github.com/Walnux/Arrow_Documents/blob/master/hypervisor/MicroHypervisor.md)"


Arrow can greatly decreases the overhead of running every single task on individual kernel and hypervisor. The performance is approaching that of container technology.

The bonus of using Hypervisor is platform(CPU Architect) and (Operating) system agnostics. Arrowized Applications can run on all the other system running Arrow infrastructure. Running on the same architect(like X86) and different system(like Windows and Linux), with KVM technology, it does not have any noticable performance impact(ToDo Add data link to prove it). [KVM Technology](https://www.linux-kvm.org/page/Main_Page).     

Besides, Arrow single task kernel is basing on standard upstream Linux kernel which is POSIX compatible. So the applications running on Linux/Unix system can be easily Arrowzied and run as Arrow.

While container working load is system and platform relevent, users have to spend efforts to develop and maintain different version of containerized working load for different plaform and system.

The dynamical linked is removed from Arrow applications. Since dynamic link is usless to single task philosophy. That will bring some limitation. Please See detail on [Arrow limitaion](/path/to/Arrow_Limitation)

## Where Arrow can be used
### cloud
### edge
### sandbox
### native
### embedded

## Limitation
