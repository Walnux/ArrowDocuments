# Limitation of Arrow Technology
Despite of the benefits of Arrow technology, there also has some limitation on it.

## Single Task
Single Task means only support single process which is construted from the combined binary(code section, data section, elf header) with Arrow kernel. It can suppor multiple threads. Golang routine can run verywell.

Starting another processs(application) on the run is not supported currently. Although in theory, it can be supported. But that will make Arrow more complicated. I have not find strong reason to support. Let's go and see.
## Static Link Only
To use Arrow technology, application must be compiled staticly.
Obviouly, staticly compiled application become more and more popular especially in cloud/netowrk/server invironment. Golang and MUSL are good example. Static link is their sale point.
And many other projects also tend to support static link. The example is nodejs.

Anyway for the application released as static linked binary like most of the projects based on Golang it quite good to use Arrow. To the application that can supprot static link like nodejs. it is also good, just need to rebuild it staticlly. But to other applications can't support static link well. Arrow technology is not a good solution. But nowdays, it is obviously, static link is more and more popular.

### plugin based on dlopen()
It has some problem to use dlopen() related functions in staticly linke application. Normally, plugin is implemented from dlopen(). Let's have a look at [why Musl does not want to support dlopen](http://openwall.com/lists/musl/2012/12/08/4)

## Extra Memory Consumption From Arrow Kernel and Hypervisor

## Application Startup Speed
