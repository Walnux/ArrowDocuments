# Arrow Design Philosophy
> “Simple can be harder than complex: You have to work hard to get your thinking clean to make it simple. But it’s worth it in the end because once you get there, you can move mountains.”

> ― Steve Jobs

In order to make cloud simple, the Application Central design philosophy is used by Arrow. Before introduce this philosophy, let us start from the System Central solution.

## System Central Solution
In nowadays, most of the applications running on Cloud evolved from the Personal Computer(PC) and Physical Server era when the full feature Operating System(OS) including OS Kernel, Middleware, libraris, tools, OS services has to be installed and started on a PC or Server before the applications can run on it.

We are in cloud era. In order to provide the conherent running environement for the applications running on cloud. The full feature OS which is called guest Operating System must be packaged with users' applications and then be deployed and run on the Cloud infrastructure. This is how cloud works. People normally call the package running on cloud as the workload.  Obviously these workloads must be based on the guest Operating system. This solution is called system central solution. 

## The Problems of System Central Solution
Although the full feature guest Operating system provides the conherent environemnt for applications to run, tools and services for the developers to develop applications and for the operators to manage the workloads, it does bring a lot of problems.

- **Wasting resources** - Obviously only part of the system resources are really needed by the application. From below diagram, we can simply understand a system central workload as a pyramid since each layer only uses part of the resources of the layer it is based on. You can image how much resources are wasted with so many this kind of pyramids running on cloud.
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/PackageInSysCentral.png">
</p>

- **Big and compliated package** - Packaging Guest Operating system with the applications you want to run on cloud leads a big package size. Further more,  it makes the software stack in the workload quit complicated to maintain.  This causes a lot of other problems. 
- **Security issues** - The extra system components increases the attacking interface number; They also can be easily used to reinforce an attack by a malicous applications, if it acquires system control priviligy; The potential system security holes in the extra compoments will all be inherited and inlcuded into the system central workload. The volunrability of cloud was increased a lot.  
- **Be difficult to do the security updates** - Firstly, it is not easy to locate and fix a security problem in the system scope. Secondly, the mechanism to do the security updates on a system is very complicated. When the system is running several applications and shared by mulitple developpers, the situation becomes worse.
- **Be difficult to share the same software among workload** - Actually, the same set of popular sofwares are repeatly packaged into different workload, shipped, deployed and running on the cloud. The traditional [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle)) combine to provide the webserver service is the good example. That wastes the overall cloud resource. Even these workloads are running on the same HostOS, it is not easy for us to break the boundary of the package to share the same set of softwares. See an example in below diagram.  Applicaton G, and B are packaged into different workload twice.  
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/AppShareSystemCentral.png">
</p>

- **Long Latency** - It definitly impactes the latency to run an application on cloud by shipping, deploying and starting the big size of full feature Client Operating System.

- **Low efficiency for team cooperating** - Users tend to package serveral applications and run them in the same guest system. These applciations may come from diffrernt owners in the same team or orgnization. System central solution impactes team members cooperating efficiency. Any modification of the system like configuration, software version from one application may influnce the other applications on the same guest system. Furthur more, the crash of the system caused by one application  will influce all the other applications on the same guest system. That influences the team or orgniztion working efficiency.
- **Increasing Operation burden** - The big and complicated packages are not easy to be managed and orchestared.  

## Application central philosophy
In stead of packaging, shipping, deploying and running applications together with a Guest Operating System on cloud, could we just directly run the applications without caring about the system and package? It is the goal of Application central philosophy.

The Application Central Philosophy based solution can be summarized as below:

- An application can directly run on cloud infrastructure indepandantly without a guestOS.
- Single application instance runs isolatedly in a sandbox.
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
- **Small software binary** - Do not need to pakcage software with the full feature GuestOS. The software binary can be very small.
- **security** - Individual single application running in sandbox isolatedly is the safest way to run application on cloud. Besides the removing of the unnecessary components also enhance the security.
- **Be easy to do security updates** - it is much easy to locate, fix a security hole to a single application than do it in a system.
- **Sharing application binary naturally**
- **Enhancing the team working efficency** - The work from different team members does't influnce each other anymore. Every application is developed, debuged and run indepandantly.
- **Improving latency** - With the small and simple application binary and the sharing of the application binary, the application startup latency can be improved easily.
- **Be easy to manage and orchestrate** Obviously, It is much more easy to manage the individual single application than managing a system.

## How to implement Application Central pilosophy
Could we just run 
Application centrialized philosophy starts from the application. Only the components that are needed by the specific applicaiton is inlcuded all the other components should be removed.

In Arrow, the staticly linked application only includes the libaries the application needs; And directly combined with the tailored kernel. The rootfs which containing the shell, Dynamical libraris, tools, and services are all removed. Logially, the kernel is part of the application. Lightweight Virutal Machine only includes the minimal resources needed to run the application.

Arrow only runs single application, it makes the applicaiton runs very safely.
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/Topdown.jpg">
</p>
Nowadays, with the development of lightweight Virtual Machine technogy, Microservcies archieture, Serverless technology and FaaS technoloy, we actually need cloud more "Application Centrialized".

Application Centrialized cloud is also be called as serverless which means just run the application on cloud safely fast with very little overhead, and don't care about the OS, middleware, libraies, image to run a server anymore.

Obviouly, changing the pyrimids to arrows makes cloud small, safe and swift. Arrow is designed to support the next generation Application Centrailized serverness cloud infrastractrue. At same time Arrow can also run the traditional LAMP stack well. 

With the Applicaiton Centralized design phynosophy, the Arrow System - the end to end solution to run Arrows on cloud is designed.
[See Arrow System Vision](/ArrowSystemVision.md)
