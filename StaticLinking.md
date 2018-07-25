# Arrow Using Staticly Linked Appliation
## what are dynamic and static linking?
according to [linker, dynamic and static linking](https://kb.iu.edu/d/akqn)

> Static linking is the result of the linker copying all library routines used in the program into the executable image. This may require more disk space and memory than dynamic linking, but is both faster and more portable, since it does not require the presence of the library on the system where it is run.

> Dynamic linking is accomplished by placing the name of a sharable library in the executable image. Actual linking with the library routines does not occur until the image is run, when both the executable and the library are placed in memory. An advantage of dynamic linking is that multiple programs can share a single copy of the library.

All in all

` "Disk", "Memory" VS "simple", "fast" and "compatible" `

At cloud/Edge/Fog enviornment, I perfer the latter. Since Simple, Fast, Compatible also means stable, robost and safe.
- The human resouces expense saving from the latter is way much bigger than the expense of Disk and memeory.
- And the expense on memory and disk is predictabe, but the expense on human resources to maitain the complicated cloud/Edge/Fog system and acquire the safity, robost and compatiblity are totoally unpredicatble  

## Why using staticly linked application

## Make static linking easier
