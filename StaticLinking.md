# Arrow Using Staticly Linked Appliation
## what are dynamic and static linking?
according to [linker, dynamic and static linking](https://kb.iu.edu/d/akqn)

> Static linking is the result of the linker copying all library routines used in the program into the executable image. This may require more disk space and memory than dynamic linking, but is both faster and more portable, since it does not require the presence of the library on the system where it is run.

> Dynamic linking is accomplished by placing the name of a sharable library in the executable image. Actual linking with the library routines does not occur until the image is run, when both the executable and the library are placed in memory. An advantage of dynamic linking is that multiple programs can share a single copy of the library.

All in all

` "Disk", "Memory" VS "simple", "fast" and "compatible" `

At cloud/Edge/Fog enviornment, I perfer the latter. Since Simple, Fast, Compatible also means stable, robost and safe.
- After many years working on Linux Distribution work, I got to know that the efforts to maintain the basical libraries like libc requires an immense amount of time and energy. Upgrade these Dynamical libraies can have unintended and sometimes catastrophic effects to the applications depending on them, so every single upgrade of these libraries require days and days of careful testing and validation. And it is almost mission impossible to cover all the cases. So I prefer to leave this huge burden to applications vendors esecially at cloud/Edge where the upgrading is quite frequent for features and security updating. Since applications verdors know all the detail of their applications, and easy for them to do the through testing on any updates after static linking. And the efforts are limitted and predicatbile compared with doing it though system level on dynamical linked Libraris. So all in all it can save the people resource and ehance the system stablility and security. 
- The human resouces expense saving from the latter is way much bigger than the expense of Disk and memeory.
- And the expense on memory and disk is predictabe, but the expense on human resources to maitain the complicated cloud/Edge/Fog system and acquire the safity, robost and compatiblity are totoally unpredicatble  

## Why using staticly linked application

## Make static linking easier
reference:
[staticly building Python](https://stackoverflow.com/questions/1150373/compile-the-python-interpreter-statically)

## legal problem of static link
To some opensource Licenses, there have some legal problems to use static link.
- Firstly, normally, you should not staticly link your code static with GPL license code. That will contaminate your code. see
[GPLStaticVsDynamic](https://www.gnu.org/licenses/gpl-faq.html#GPLStaticVsDynamic)

- Secondly, There is _no_ legal problem to staticly link the LGPL code. The only requirement is that the application object file must be provided for end uers to link with other version of LGPL library. And the you need _not_ open your source. see
[LGPLStaticVsDynamic](https://www.gnu.org/licenses/gpl-faq.html#LGPLStaticVsDynamic).
