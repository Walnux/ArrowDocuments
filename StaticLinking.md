# Static Linking is the best choise for Clound and edge computing
## what are dynamic and what is static linking?
according to [linker, dynamic and static linking](https://kb.iu.edu/d/akqn)

> Static linking is the result of the linker copying all library routines used in the program into the executable image. This may require more disk space and memory than dynamic linking, but is both faster and more portable, since it does not require the presence of the library on the system where it is run.

> Dynamic linking is accomplished by placing the name of a sharable library in the executable image. Actual linking with the library routines does not occur until the image is run, when both the executable and the library are placed in memory. An advantage of dynamic linking is that multiple programs can share a single copy of the library.


## Pros and conts of static linking
### Comparing Table 

### Personal Experience

After several years working on Operation System Distribution, I got to know that the efforts to maintain the shared libraries is "hudge". Upgrading a dynamicly linked libraie may cause some unexpected impaction to the whole system.  In order to avoid this happening, careful validation at least the main features must be done. Some time, you even do not know what features may be influnced and should be tested because of the complicated dependency chain. So leaving this to application vendors at cloud/Edge where the upgrading is quite frequent is the best and maybe the only option. Besides, at the situation when microservice running in some isolated environment, static link is the best choise.

### In summary, static linking has benefits at every apsects except for
- Disk/Memory Size
- Plugin
At Arrow we can relief the two issues. 

## Arrow share memeory technology can make static "small"
Since with Arrow, everything is in memory. We can reduce the memory consumption by memory sharing and COW(Copy On Write) technology, when we run several Arrow instnaces at same time.

The readonly sections can be shared and writable sections are COW among several same application instances. This can save memory size a lot. And actually at cloud in order to balance working load, quite often, several same applications/services may be kicked off. 
Even difffernt Arrow Instances which uses the same Single Task kernel, several kernel sections can be shared.

this needs to be implemented through kernel and Hypervisor. 
Needs to work on Prototype 

## Statci Linking Plugin
Needs more investigation

## Make static linking easier
reference:
[staticly building Python](https://stackoverflow.com/questions/1150373/compile-the-python-interpreter-statically)

## legal problem of static link
To some opensource Licenses, there have some legal problems to use static link.
- Firstly, normally, you should not staticly link your code static with GPL license code. That will contaminate your code. see
[GPLStaticVsDynamic](https://www.gnu.org/licenses/gpl-faq.html#GPLStaticVsDynamic)

## Resources
[How SDL handle static and dynamic link](https://hg.libsdl.org/SDL/file/default/docs/README-dynapi.md)
- Secondly, There is _no_ legal problem to staticly link the LGPL code. The only requirement is that the application object file must be provided for end uers to link with other version of LGPL library. And the you need _not_ open your source. see
[LGPLStaticVsDynamic](https://www.gnu.org/licenses/gpl-faq.html#LGPLStaticVsDynamic).

[When to use dynamic linking and static linking](https://www.ibm.com/support/knowledgecenter/en/ssw_aix_71/com.ibm.aix.performance/when_dyn_linking_static_linking.htm)

[Dependency hell](https://en.wikipedia.org/wiki/Dependency_hell)
