# Arrow Design Philosophy
> “Simple can be harder than complex: You have to work hard to get your thinking clean to make it simple. But it’s worth it in the end because once you get there, you can move mountains.”

> ― Steve Jobs

[System Central Solution](#system-central-solution)

[Problems Caused by System Central Solution](#problems-caused-by-system-central-solution)

[Application Central Philosophy](#application-central-philosophy)

[The way to implement Application Central Solution](#the-way-to-implement-application-central-solution)

In order to make cloud simple, the Application Central design philosophy is used by Arrow. Before introduce this philosophy, let us start from the System Central solution.

## System Central Solution
In nowadays, most of the applications running on Cloud evolved from the Personal Computer(PC) and Physical Server era when the full feature Operating System(OS) including OS Kernel, Middleware, libraris, tools, OS services has to be installed and started on a PC or Server before the applications can run on it.

We are in cloud era. In order to provide the conherent running environement for the applications running on cloud. The full feature OS which is called guest Operating System must be packaged with users' applications and then be deployed and run on the Cloud infrastructure. This is how cloud works. People normally call the package running on cloud as the workload.  Obviously these workloads must be based on the guest Operating system. This solution is called system central solution. 

## Problems Caused by System Central Solution
Although the full feature guest Operating System provides the conherent environemnt for applications to run, tools and services for the developers to develop applications and for the operators to manage the workloads, it does bring a lot of problems.

- **Wasting resources** - Obviously only part of the system resources are really needed by the application. From below diagram, we can simply understand a system central workload as a pyramid since each layer only uses part of the resources of the layer it is based on. You can image how much resources are wasted with so many this kind of pyramids running on cloud.
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/PackageInSysCentral.png">
</p>

- **Big and compliated package** - Packaging Guest Operating system with the applications you want to run on cloud leads a big package size. Further more,  it makes the software stack in the workload quite complicated to maintain.  This causes a lot of other problems. 
- **Security issues** - The extra system components increase the attacking interface number; They also can be easily used to reinforce an attack by a malicous applications, if it acquires the system control priviligy; The potential system security holes in the extra compoments will all be inherited and inlcuded into the system central workload. Consequently, the volunrability of cloud was increased.  
- **Be difficult to do the security updates** - Firstly, it is not easy to locate and fix a security problem in the system scope. Secondly, the mechanism to do the security updates on a system is very complicated. When the system is running several applications and shared by mulitple developpers, the situation becomes worse.
- **Be difficult to share the same software among workload** - Actually, the same set of popular sofwares are repeatly packaged into different workload, shipped, deployed and running on the cloud. The traditional [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) combination to provide the webserver service is the good example. That wastes the overall cloud resources. When these workloads are running on the same HostOS, it is not easy for us to break the boundary of the package to share the same set of softwares. See an example in below diagram.  Applicaton G, and B are packaged into different workload twice.  
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/AppShareSystemCentral.png">
</p>

- **Long Latency** - It definitly impactes the latency to run an application on cloud by shipping, deploying and starting the big size of full feature Client Operating System.

- **Low efficiency for team cooperating** - Users tend to package serveral applications and run them in the same guest system. These applciations may come from diffrernt owners in the same team or orgnization. System central solution impactes team members cooperating efficiency. Any modification of the system like configuration, software version required from one application may influnce the other applications on the same guest system. Furthur more, the crash of the system caused by one application  will influce all the other applications on the same guest system. That influences the team or orgniztion working efficiency.
- **Increasing Operation burden** - The big and complicated packages are not easy to be managed and orchestared.  

## Application Central Philosophy
In stead of packaging, shipping, deploying and running applications together with a Guest Operating System on cloud, could we just directly run the applications without caring about the system and package? It is the goal of Application central philosophy.

The Application Central Philosophy based solution can be summarized as below:

- An application can directly run on cloud infrastructure indepandantly without a guestOS.
- Single application instance runs isolatedly in a sandbox.
- The application should be agnostic to Cloud infrastructure.
- The applications can cooperate with each other through standard TCP/IP network.
- Bounch of applicatons instances work together to implement a cloud service.
- Different Cloud services reuse the same application binary.
- Runing the application on cloud infrastrucure should be very simple.
- The mainstream applications on cloud do not need to be ported or modified to run

The system central solution model can be demostrated as below diagram.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/AppShareAppCentral.png">
</p>

With application central solution, the current problmes caused by system cnetral solutions can be resolved very well.
- **Using resources efficiently** - Only the resources that really need by the Application will be included and assinged.
- **Small software binary** - Users do not need to pakcage software with the full feature GuestOS any more. The application binary can be very small.
- **security** - Individual single application running in sandbox isolatedly is the safest way to run application on cloud. Besides the removing of the unnecessary components also enhance the security.
- **Be easy to do security updates** - it is much easy to locate, fix a security hole to a single application than do it in a system.
- **Sharing application binary naturally**
- **Enhancing the team working efficency** - The work from different team members does't influnce each other anymore. Every application is developed, debuged and run indepandantly.
- **Improving latency** - With the small and simple application binary and the sharing of the application binary, the application startup latency can be improved easily.
- **Be easy to manage and orchestrate** Obviously, It is much more easy to manage the individual single application than managing a system.

## The way to implement Application Central Solution
Obviously, traditional Virtual Machine technology is not suitable for Application Central Solution.

Dockerized container technology looks like the solution dawn. Using the small size GuestOS like Alpine, it shrinks the package size a lot; By shareing the same Host kernel, it uses system resources more efficienctly; Using unionFS, it shares software binary in some degree. Most importantly, it is the end to end solution and designed to be easy to use. 

However, it is not suitable for Application Central Solution.
- Container is not the sandbox, and can't provide the firm and secure enough isolating environment for applicaiton to run. 
- Docker Container system is too heavy to pakcage a single application. Since it is desinged mostly to package a software system.
- The Unionfs used by Docker container can be used to share the software, but it impacts the performance. And the software sharing can't be proved. We know the unionFS layers mechanism is quite heavy and complicated. The same software can be shared only when they are exactly based on the same layer.
- Any intention to enahce the security of Container may brake the simplicity and efficiency of original design.
- To share the hostOS kernel, the applicaiton can't be run agnosticly cloud infrastructure.

Unikernel is suitable for Application Central Solution but may not be fit for production.

[Unikernel](https://en.wikipedia.org/wiki/Unikernel) runs single application on the Hypervisor on cloud. It aligns with the Application Central philosophy. But [Unikernel may not be fit for production](https://www.joyent.com/blog/unikernels-are-unfit-for-production).
- Applications and the Libraries have to be ported, rebuild and link with a libOS and run on the Hypervisor. The problem is that all the mainstream Applications are developped and running on the standard mainstream Operating system like Linux. So it will take big efforts for any Unikernel solution to run all the mainstream cloud Applications properly and reach the production quality.
- Some people are trying to resolve the problem by [changing the standard Linux kernel into a Unikernel LibOS](https://www.researchgate.net/publication/332329656_Unikernels_The_Next_Stage_of_Linux's_Dominance). This solution may meet legal risk. Kernel code is released under GPLV2 License. If an application links with these code which are covered by GPLV2 License, there may exist some [legal problem](https://www.gnu.org/licenses/old-licenses/gpl-2.0-faq.en.html#LinkingWithGPL).   
- Unikernel only supports single process while some Cloud applications are multi-process framwork. The good example is the wellknown webserver application Nginx.
- In order to promote the performance, Unikernel uses the flat applicaiton memory space and removes the Ring transition. While [Userspace](http://www.linfo.org/user_space.html) and [kernel space](http://www.linfo.org/kernel_space.html) split as well as [Protection Ring machanism](https://en.wikipedia.org/wiki/Protection_ring) are the fundamental security mechanism for moden Operating System. Malicous user applications runing with the kernel code in the same memeory space with Ring0 - the highest running priviligy can directly attack the Hypervisor as well as the HostOS.
- Finally, till now, we didn't find a production quality end to end unikernel solution for user to run and manage their applications on cloud.

[**Arrow is desinged and implemented for Applicaiton Central Solutions**](/README.md). 
