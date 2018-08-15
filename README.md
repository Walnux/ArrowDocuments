# Arrow Overview
Other than Virtual Machine and Container technology, Arrow provides another safe, fast, small, easy, agnostic and compatible  way to package, release, deploy, run, manage and orchestate tasks in cloud, edge, native, even embedded environemnt.

Arrow technology is application centralized. Unlike running an operating system on Virtual Machine, or running tasks in Container, Arrow itself is the task. With [Arrow infrastructure(Arrow service)](/path/to/Arrow_Infrastructure), user can run Arrowized application as easy as running a normal application. What different is that all the Arrowized applications are runing in "fully" isolated environemnt. They also can be connected with each other through TCP/IP based Arrow Network. Since Arrow infrastructure is desgined to compatible with Container(like Docker container) and container orchestartion system like Kubernetes. Arrow can be easily integrated into Kubernetes and seamless cooperate with the existing Container infrastructure.

Arrow provides a very safe way to run user application, since each application combine and runs on its own tailed single task kernel which exactly matches the requiremnts of the application. At same time the single task kernel runs on the highly configured Hypervisor like Qemu-KVM or Nemu-KVM.[See Arrow Design Philosophy](/path/to/Arrow_Philosophy) The combination of static application with tailed kernel greatly increase the security by reducing the number of attacking interfaces. And single task kernel running on Hypervisor provides throughly isolation for each application. So obviously, with Arrow technology, users can running their tasks safely and stably. 

Arrow is small and fast approaching the performance of container technology. With the innovative "[Application Loader & single task Kernel](/path/to/Arrow_Application_Loader_Single_Task_Kernel)", "[Kernel Sharing](/path/to/Arrow_Kernel_Sharing)", "[In-memory Filesystem](/path/to/Arrow_In_memory_Filesystem)" technologies and making use of non-simulation Hypervisor, Arrow can decreases the overhead of running every task on individual kernel and hypervisor to the lowest level.

The bonus of using Hypervisor is that the application is platform and system agnostics. Arrowized Applications can run on all the other system with Arrow infrastructure. Running on the same architect(like X86) and different system(like Windows and Linux), with KVM even does not have any noticable performance impact(ToDo Add data link to prove it). [KVM Technology](https://www.linux-kvm.org/page/Main_Page).     

Besides, Arrow single task kernel is basing on standard upstream Linux kernel. So the applications running on Linux can be easily Arrowzied and run as Arrow.

While container working load is system and platform relevent, users have to spend efforts to develop and maintain different version of containerized working load for different plaform and system.

Arrow still has some limitations. In order to decrease the overhead, the dynamical linked applications currently are not supported by Arrow. See detail on [Arrow limitaion](/path/to/Arrow_Limitation)

## Where Arrow can be used
### cloud
### edge
### sandbox
### native
### embedded

## Limitation
