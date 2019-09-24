# Standard Linux Kernel based Single Task Kernel
## What is Single Task Kernel
Single task kernel is based on starndard Linux Kernel which is optimized and tailored for a single applicaiton to run. The single application can be any applications running on linux Operating System. The only 2 limitations for the application are:

* It must be staticly linked. For the kernel only runs a single application, there is no reason to keep the complication of the Dyanmically Linked Library. Staticly linked application only includes the code the application really needs. Basing on the asumption that only statically linked application supported. A [lot of innovations](/TechnologyBlueprint.md) can be work out to make Arrow simple, safe, fast and small basing on the standard Linux kernel.   

* Could not start up another application




Single Task Kernel retains all the advantages of Linux like the battle tested code base, hudge open source community and vast supporting of legacy software
