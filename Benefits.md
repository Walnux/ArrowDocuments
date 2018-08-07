# Why Using Arrow

## Usage area
### serverless Faas Micro-Service
### Edge Computer
## Key Technologes
### Appliation loading is faster and low latency
Arrow image which combines application with kernel is loaded into memeory by VM(Qemu-kvm) as a single file(Single DMA operation in IO). It is much faster and simple than the traditional VM application loading, which requires to start kernel and then mount the rootfs from a image file on host disk or through network protocoal based Filesystem(like 9P). And then load the application through a very complicated and long procedure including loading and parsing file header, load and build the process by creating all the necessary segemnts through lazy mmap() mechanical. The mmap() mechnical will just mmap the segements to specific binary file, and not actually read and load it into memory. Once program run into some code that is not in memory, the segmentation exception happends and guest Kernel will kickof disk IO operation all the way to the file on physical disk by the helping of host Kernel Filesytem and disk IO,  and read the applicaiton binary data from the physical disk and load it all the way back to guest OS and finish the applicaiton data loading and memory map constrution and then applicaiton can resume from the applicaiton semgment execetion falt and then resume to run. That is a very very slow and expensive procedure. if the host disk IO is very busy the latency can't be estimated. That is the main reasone why the Virtual machine and guest OS must include the heavy and slow disk IO, file system module and disk simuation module. These modules which makes the VM and Guest very big and slow.  See Xen Hypervisor disk io architecture figure from the [virtula Machine Xen disk IO](https://ac.els-cdn.com/S0022000012000980/1-s2.0-S0022000012000980-main.pdf?_tid=e518d902-0cc0-4c25-a923-18fbeb5e73fc&acdnat=1532536951_d6469936df6e82096486440e7796ea16) (The basical mechanical of linux and qemue-kvm currently used by Arrow is quite simiar with Zen hypervisor)
![Xen Hypervisor disk io architecture](/images/Disk_I_O_architeture_of_Xen.jpg)
So obviously, the normal VM application loading and disk IO is very slow.

Let looks at the moden Micro-Service architecture, normally the most of the services do not need to access the disk except loading the service itself, and the loading some configure files or keys(at Arrow, they are called as applicaiton meta data). Kubernetes and Edgex are the good examples. in Kubernetes the main services like kube-apiserver, kube-contoller-manager and kube-scheduler actually never access the disk, all the data are stored into etcd through network. and Edgex is quite similar. With This kind of excellent design. Using Arrow loader, and Arrow meta-data filesystem technology, we can totally remove the heavy and slow disk IO, Filesytem module in guest OS and disk simulation module in Hypervisor.

So it is `Fast Simple and Small`
So it is quite valuable at the usage case require "low latency"

The concern is that will increase the memory consumption by reading all the applicaiton data into memeory. That acutally is not the problem, using the tradional way, you just lazy load the memory, soon or later all the applicaiton data will be load into the memory. The Arrow loader just make application loader simple and fast.

![Arrow Application Loader](/images/ArrowAppliationLoading.jpg)

### In Memory Filesystem Technology

### Kernel Sharing Technology

### Arrow Infrastrucutre Technology

## Security

## Stable

## Small

## Platform and Operating System agnostic
Unlike Containers working load can only run on some specific Operating System, with the help of hypvisor and Arrow framwork like Crossbow and Arrowd, the Arrow image can run on different Operating system and platforms. So it is platform and Operating system agnostic.

In theory with KVM runing X86 based Arrow image on Windows and Linux host have the simiar performance. Runing on ARM platform may expect some performance sacrifice, becuase Hypervisor has to simulate and translate the X86 code to ARM code. 

So suggust to run Arrow image on the same architecture platform. Currently X86-64 is the prefered and suggest architecutre platofrm. 

## Customerized Kernel
Unlike Containers working load sharing the same kernel. With Arrow, users actually has the free to Arrowize their applications with the customerized kernel. That is quite helpful, if users want to integrate using and release their own developped kernel modules or kernel configure.
