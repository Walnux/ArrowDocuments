# Arrow Design Philosophy
> “Simple can be harder than complex: You have to work hard to get your thinking clean to make it simple. But it’s worth it in the end because once you get there, you can move mountains.”

> ― Steve Jobs

In order to make cloud simple. The Application Central design philosophy is used by Arrow. Before introduce this philosophy, let us start from the System Centrial solution.

Most of the applications running on Cloud evolved from the Personal Computer and Physical Server era when the full software system including Operating System Middleware libraris, tools, services as well as applications ever runs on physical servers are packaged into images and migrated to run on Virtual Machines.

We know, the goal for users to buy the physial servers or rent the virtual machines is to run the applicaiton. However, in order to run application, they have to install the Full feature Operating System on the machine (physical server or virtual machine), and then install the middleware, libraries services and tools and then can install and run the application on it. Obvisouly, OS only uses part of resources provided by the machine, middleware/services/libraries only uses part of resources provided by OS, and applicaiton only uses part of resources provicded by middleware/services/libraries. System centralized solution has to provide a full feature system to support all the possible applications. Each this kind of system is a pyramid as showed in below figure. And on cloud, there runs independant huge numbe of pyramids.

Although the full feature guest system provides the conherent running environemnt for applications and developers, it brings a lot of problems.

- Wasting resources - Since only part of the system resources are really needed by the application.
- Security - The extra system software components increases the number of attacking interfaces; They also can be used to reinforce an attack by malicous applications more easily; The potential security hole in the extra compoments are inherited.
- Big package size - obviousely, it leads a big package size.
- Not easy to share software among packages - Actually, a lot of same set of sofwares are repeatly included into different systems. That wastes the overall cloud resource.
- latency - It is not easy to reduce the latency to deploy and run the big packages.
- Efforts to team cooperation - Quite often, serveral applications run in the same guest system. These applciations may come from diffrernt owners in the same team or orgnization. Any modification of the system like configuration, software version influnces the others. Even worse, the crash of the system from one application may influce all the other applications.     
System config and software version change have to be synchnized among all the applicaitons from differnt    
- Increasing Operation burden - The big and complicated system packages is not easy to be managed and orchestared.  

Obviously, a lot of resources are wasted. Although Container can package a single application, most of workloads in containers are actually ported from the virtual machine System Centrialized image.
![BottomUp](/images/BottomUp.jpg?raw=true "BottomUp")

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
