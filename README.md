# What is Arrow?
Arrow is the "Single Task OS(Operating System)", which means the OS only runs single task. Here single task means single Process which can contain several threads.
Compared with the traditional OS which can run several tasks processes, which can be managed in sessions, process groups, and Process name spaces. "Single Task OS" is quite strait forward and simple since only one process running on the OS. 
At same time "Single Task OS" is the application centrailized OS. In theory, the OS only include what needed by the single application running as a single process. 

# Arrow Overview
Other than Virtual Machine and Container technology, Arrow provides another safe, fast, small, easy, agnostic and compatible  way to develop, package, release, deploy, run, manage and orchestate tasks in cloud, edge, native, even embedded environemnt.

Arrow technology is application centralized. Unlike running an Operating System on Virtual Machine, or running tasks in Container, Arrow itself is the task the applicaton or the service. With [Arrow service)](/path/to/Arrow_Infrastructure), user can run Arrow as easy as running a normal application.

What different is that all the Arrowized applications are runing in "fully" isolated environemnt. They can be connected with each other through TCP/IP based Arrow Network. Since Arrow infrastructure is desgined from begining to be compatible with Container(like Docker container) and container orchestartion system like Kubernetes. Arrow can be easily integrated into Kubernetes and seamless cooperate with the existing Container infrastructure.

Arrow provides a very safe way to run user application, since each application combine and runs on its own tailed single task kernel which exactly matches the requiremnts of the application. At same time the single task kernel runs on the highly configured Hypervisor like Qemu-KVM or Nemu-KVM.[See Arrow Design Philosophy](/path/to/Arrow_Philosophy) The combination of static linked application with tailed kernel greatly increase the security by reducing the number of attacking interfaces. The single task kernel running on Hypervisor provides throughly isolation for each application. Obviously, with Arrow technology, users can run their tasks safely and stably. 

Arrow is small and fast. With the innovative technoloies like:

- "[Application Loader & single task Kernel](/path/to/Arrow_Application_Loader_Single_Task_Kernel)", 
- "[Kernel Sharing](/path/to/Arrow_Kernel_Sharing)",
- "[In-memory Filesystem](/path/to/Arrow_In_memory_Filesystem)",
- "[Micro Hypervisor](/path/to/Micro_Hypervisor)"


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
