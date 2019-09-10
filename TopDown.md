# Arrow Design Philosophy

Arrow is based on Application Centrialized design philosophy. Before introduce this philosophy, lets start from the System Centrialized solution

Cloud was evolved from the physical servers to Virtual Machines. The full software system including Operating System Middleware libraris, tools, services as well as applications ever runs on physical servers are packaged into images and migrated to run on Virtual Machines.

Although Cloud technology envolved from Virtual Machine to Container. The System Centrialized solution is still be widely used.

We know, the goal for users to buy the physial servers or rent the virtual machines is to run the applicaiton. However, in order to run application, they have to install the Full feature Operating System on the machine (physical server or virtual machine), and then install the middleware, libraries services and tools and then can install and run the application on it. Obvisouly, OS only uses part of resources provided by the machine, middleware/services/libraries only uses part of resources provided by OS, and applicaiton only uses part of resources provicded by middleware/services/libraries. System centralized solution has to provide a full feature system to support all the possible applications. Each this kind of system is a pyramid as show in figure. And on cloud, there runs huge numbe pyramids. Obviously, a lot of resources are wasted. Although Container can package single application, most of workloads in containers are actually ported from the virtual machine System Centrialized image.

Application centrialized philosophy starts from the application. Only the components that are needed by the specific applicaiton is inlcuded all the other components should be removed.

In Arrow, the staticly linked application only includes the libaries the application needs; And directly combined with the tailored kernel. The rootfs which containing the shell, Dynamical libraris, tools, and services are all removed. And run it on the lightweight Virutal Machine which only include the minial resources needed to run the application.    

Nowadays, with the development of lightweight Virtual Machine technogy, Microservcies archieture, Serverless technology and FaaS technoloy, we actually need cloud more "Application Centrialized".

Application Centrialized cloud means just run the application in cloud and care about the OS, middleware, libraies, image, Machine and so on and also make sure the applicaiton is run securily.

Obviouly, changing the pyrimids to arrows makes cloud small, safe and swift.

![Topdown](/images/Topdown.jpg?raw=true "Topdown")
