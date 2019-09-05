# What is Arrow?
**Arrow is the application.**

The application is combined with the tailored single task kernel running on the lightweight Virtual Machine.

Arrow is designed basing on the [**Application Centrialized Top Down**](/path/to/topdown) design philosophy.

Applications can be run as Arrows on cloud, edge computing and native computer safely, simply and swiftly.

**Arrow System** is the end to end solution to run and manage Arrows


# Arrow Overview
Arrow is the application [which can be run](/path/to/example) as simply as a normal application natively. Arrows are designed to for Microservice. They can be orchestrated to work together to fullfill the specific goal with Kubernates in cloud environment. Arrow also can be integrated into users' FaaS solutions.

The single application is combined with the tailored single task kernel running on the Virtual Machine. So the application actually runs isolately in the sandbox. Besides, all the unnecessary components like Dynamical Libearis, Shell, tools within rootfs, even the rootfs itsef and the kernel block devices and specific filesystem components and application loader to run applications and so on are all removed. Only single application can run just onetime in the single task kernel.

Obviously, Arrow is the secure way to run application.
- Firstly, Arrow runs single applicaton isloated in the sandbox.
- Secondly, by removing all the unnecessary components, the attack interface in each Arrow is reduced greatly.
- Third, even Arrow is hacked, it is very difficult to be manipulated to attack or hack others, since Arrow can only run sigle applicaton one time, and the resources can be used are very limited.   

The single task kernel is based on Linux kernel. And the application runs in the stardard Linux environment. So all the applications running on Linux can run as Arrow with [very few limitations](/path/to/limitation). Abundant Linux applications can run as Arrow with help of [ASDK Arrow System Development Kit](/path/to/ASDK).

Swift means small, fast and flexible.

- **Each Arrow only needs < ~1M memory overhead**

With [Application Centrialized Top Down](/path/to/topdown) design philosophy, and [lightweight Virtual Machine](/path/to/lightweithtVirtualMachine) technology for moden cloud and edge computing usages, several [foundmental innovations](/path/to/innovations) are worked out for Arrow to [run application with very small overhead](/path/to/overhead). 

- **Arrow is very small and shared with all the users

Arrow is the applicaton combined with single task kernel running on lightweight Virtual Machine, as mentioned above, it only contain the necessary binary segments which can be preinstalled or intalled ondemand and shared by all the users. At most situations the Virtual Machine with the single task kernel can also be shared by all the users. Besides, Arrow is desinged seperated from data and configuration. the only thing needs to ship is the configurations as well as the stateful data used to setup the environemnt or mirgration of the stateful applications.

- **Arrow application loading latency approaches native application loading

Arrow itself is very small and can be preinstalled so the loading latency is small, further more, the [Arrow template and clone technology](/path/to/AtemplateClone) technology and [Arrow application sharing](/path/toAshareing) technology makes Arrow application loading latency approach native application loading.

-- **Arrow is single application and quite flexible and easy to be orchestrated**
 
 Compared with the heavy full OS stack Virtual Machine or Container workload, Arrow is quite flexible to be managed and orchestrated and shared. Since it is the small single application. So it is natively suitable for microservice architecture. And most important is that the single application can be shared by all the users flexiblely. So users do not need to include the same applications in their individual workload.  

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
