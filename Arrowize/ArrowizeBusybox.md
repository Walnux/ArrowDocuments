# Arrowize Busybox
[Busybox](https://busybox.net/about.html) is the the Swiss Army Knife of Embedded Linux.
Arrowize Busybox, you can get the world's smallest linux with the most amazing features.

## Build your staticly linked Busybox image

## Arrow technology and Busybox
Busybox is the true Swiss Army Knife of Embedded Linux. It integrate nearly all the gerneal linux features/tools into one binary, and identify the feature user want to use through link name. the link name will be saved at argv[0] as the command name. Arrow populate the argv[0] with command name. so that is compatible with Busybox. so you can run Arrowized Busybox like
` #crossbow run busybox sh ` [see crossbow user manual](https://github.com/Walnux/Crossbow/blob/master/Manual.md)
Busybox is the ideal tools to debug the Arrow kernel.

## Arrowize 
