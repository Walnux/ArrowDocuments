# Arrow System Vision
## Arrow only runs Applications on cloud

Arrow only runs applications. It dosen't pakcage and ship applications like what Virtural Machine and Container do. 

Virtural Machine Image and Container Image are designed to package and ship softwares which are normally in some kind of OS like Alphine or Ubuntu. The reality is many images tend to be big and redundant. That impacts software loading latency, wastes network bandwith and storage resource. Deep dive into these images, we can easily find that actually same set of softwares are reaptly packaged and shipped by many different users. These softwares include base OS, Javascript Runtime(nodejs), Python Runtime(cpython), Nginx, MogoDB, MySeql, Redis and so on. Could we decrease the image overhead by shrinking the size of images and sharing the same softwares shipped by different images to save storage resource and promote the application loading latency? Could we run applications on cloud just as easily as run applications on native Computer and at same time keep them safe?

As mentioned in the [Application Centrialized Design Philosophy](/TopDown.md). Arrow combines the staticly linked single application binary with the single task kernel and runs it on lightweight Virtual Machine. The "image" needs to load is only the staticly linked binary which is very small. The single task kernel with the lightweight Virtual Machine normally are same (with different configure) to many Cloud applications. So they can be shared through [Arrow template and clone technology](/path/to/TemplateClone.md). Further more on the same physical node, the same staticly linked applications instance can be loaded using [Arrow Application Loader](/path/to/Aloader.md) technology from the same binary file. So the overhead and latency to load application on cloud is decreased.

Users can use [Arrow Service](/path/to/ArrowService.md) to [run Arrow instance](/path/to/LifeCycle.md) very easily. It runs the single application in the isotlated sandbox provided by the lightweigh Virtualmachine. Arrow Service also configure [Arrow networks](/path/to/ArrowNetwork.md) for Arrow. So Arrows can connect with each other or with outside easily.

Arrow system can also be hooked into Kubernetes systems and orchestated as the cloud workload.

## Arrow Ecosystem
Arrow doesn't package and ship applications. Arrow run single Application. Since the single application is very small.  The widely used Arrow applications as well as tailed Arrow kernel templates can be preinstalled as part of hostOS or pulled from the Arrow repository ondemand. These are called as the system Arrows. Normally system Arrows is released and maintained by ASV (Arrow System Vendor). Users can just run it using Arrow System and merge it into users usage. User can also release their own Arrow applications from Arrow user repositoris. The Arrow will be pulled and run by Arrow system on demand.

Arrow is designed to seperate the application with configuration and data. The Arrow data and configureation is handled by [Arrow ShadowFS](/path/to/ShadowFS.md).

[ASDK Arrow System Development Kit](/path/to/ASDK.md) is used to build Arrow applications. 
![ArrowEcosystem](/images/ArrowEcosystem.jpg?raw=true "ArrowEcosystem")

## Docker Container Sharing 
Making use of Unionfs technology, Docker container mitigate the problem by sharing some layers. But these sharing comes with restriction. Only when the same layers are based on the same base layer and installed with the same order, they can be shared among images. For example, two container images package the same set of softwares A, B based on baseOS. If they package with same order like (BaseOS, A and B). They can share the layers. However, if they are pakcaged with different order like (baseOS, A, B) and (baseOS, B, A). They have totally different layers and can't share. We never can restrict the package order. Docker container can't fully share softwares among images. So that impact the image size and container loading efficency.

Besides,  we know that the unionFS itself is complicated and slow.
