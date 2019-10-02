# Arrow Design Philosophy
> “Simple can be harder than complex: You have to work hard to get your thinking clean to make it simple. But it’s worth it in the end because once you get there, you can move mountains.”

> ― Steve Jobs

In order to make cloud simple. The Application Central design philosophy is used by Arrow. Before introduce this philosophy, let us start from the System Centrial solution.

## System central solution
Most of the applications running on Cloud evolved from the Personal Computer and Physical Server era when the full feature Operating System(OS) including OS Kernel, Middleware, libraris, tools, OS services has to be installed before the applications can run on it.

In order to provide the conherent running environement for the applications running on cloud. The full feature OS which also be called guest system must be packaged with these applications and then deploy and run on the Cloud infrastructure. People normally call the package running on cloud as cloud workload.  Obviously these workloads are basing on the guest system. it is the system cential solution. From below diagram, we can simply understand a system central workload as a pyramid since each layer only uses part resources of the layer it is based on.  
![BottomUp](/images/BottomUp.jpg?raw=true "BottomUp")

## The problems of system central solution
Although the full feature guest system provides not only the conherent running environemnt for applications but also tools for the developers, it brings a lot of problems.

- Wasting resources - Since only part of the system resources are really needed by the application.
- Security issues - The extra system software components increases the number of attacking interfaces; They also can be used to reinforce an attack by malicous applications more easily; The potential security hole in the extra compoments are inherited.
- Be difficult to do the security update - Firstly, tt is not easy to locate and fix a security problem from the system scope. Secondly, the mechanism to do the security update on a system is complicated.
- Big package size - obviousely, it leads a big package size.
- Be difficult to share the same software among systems - Actually, the same set of sofwares are repeatly packaged into different guest systems running on cloud. That wastes the overall cloud resource.
- Long Latency - It impactes the latency to deploy and run the big size of full feature system.
- Low efficiency of team cooperation - Users tend to package serveral applications and run them in the same guest system. These applciations may come from diffrernt owners in the same team or orgnization. Any modification of the system like configuration, software version from one application may influnce the other applications on the same guest system. Even worse, the crash of the system caused by one application influces all the other applications on the same guest system. That influence the team or orgniztion working efficiency.
- Increasing Operation burden - The big and complicated system packages is not easy to be managed and orchestared.  

## Application central philosophy
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
