# Arrow Design Philosophy

Arrow is based on Application Centrialized design philosophy. Before introduce this philosophy, lets have a looks at the System Centrialized solution

Cloud was evolved from the physical servers to Virtual Machines. The full software system including Operating System Middleware libraris, tools, services as well as applications ever runs on physical servers are packaged into images and migrated to run on Virtual Machines.

Although Cloud technology envolved from Virtual Machine to Container. The System Centrialized solution is still be widely used.

We know, the goal for users to buy the physial servers or rent the virtual machines is to run the applicaiton. However, in order to run application, they have to install the Full feature Operating System on the machine (physical server or virtual machine), and then install the middleware, libraries services and tools and then can install and run the application on it. Obvisouly, OS only uses part of resources provided by the machine, middleware/services/libraries only uses part of resources provided by OS, and applicaiton only uses part of resources provicded by middleware/services/libraries. System centralized solution have to provide a full feature general system to run all the possible applications. Each this kind of system is a pyramid. And on cloud, there runs huge numbe of this kind of pyramids. A lot of resources are wasted. It makes the cloud infrastructure redunant and complicated. Although Container can package single application, most of workloads in containers are actually ported from virtual machine image and keeps System Centrialized.

With the development of lightweight Virtual Machine technogy, Microservcies archieture, Serverless technology and FaaS technoloy, instead of system centrialized soluiton, we actually can make cloud more "Application Centrialized".

Application Centrialized cloud meands Just run the application you want to run on cloud and do not need to care about the OS, middleware, libraies, image, Machine and so on and also make sure the applicaiton is run securily.

Firstly, The application is saticly linked with only the codes it really needs. The Dynamical Libraris are removed.
Secondly, The application directly combine with the tailored single task kernel and the whole rootfs which includes shell, tools, services are all removed
Third, the kernel is tailored to the application, all the unused components like block deivces, the backed filesystems and the application load are removed.
Lastly, Arrow runs on the lightweight Virtualmachine which only include the basic network and serial ports.

Obviouly, changing the pyrimids to arrows makes cloud small, safe and switf.
