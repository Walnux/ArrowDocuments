# Running Busybox as Arrow Instance

## Arrow and Busybox
Busybox is the true Swiss Army Knife of Embedded Linux. It integrates nearly all the general linux features/tools into one binary, and identify the feature user want to use through link name. the link name will be saved at argv[0] as the command name. Arrow populate the argv[0] with command name. That is compatible with Busybox design.

Busybox is the ideal tools to debug Arrow Single Task Kernel. Running Busybox as Arrow Instance, actually, you might be using the smallest Linux in the word.

In Arrow 0.1 Release. Busybox has been integrated into [ASDK](Walnux/Atools/tree/master/ASDK). You can use ASDK to build "Combined Mode" Busybox Arrow Image and run it as Arrow Instance through [Arrow Service](arrowd/edit/master/README.md). 

## How to Run Busybox as Arrow Instance
- After setting up [ASDK](Walnux/Atools/tree/master/ASDK) and [Arrow Service](arrowd/edit/master/README.md). And Arrowd has been started. You can run Busybox as Arrow Instance in Arrowd source directory:

```shell
$ sudo ./bin/actrl shoot -t busybox sh
```

- Using below command to check the Arrow applications running statues

``` shell
$ sudo ./bin/actrl list
busybox bpfaeddd5h2u8e3q7svg    sh      sh      io.arrowd.arrow.status.running.v1
```

- Using below command to attach your STDIO with your terminal

``` shell
sudo ./bin/actrl attach

/ # ls
data  dev   etc   proc  root  sys   tmp
```

- Using ifconfig command to check the network configure

``` sh
/ # ifconfig
eth0      Link encap:Ethernet  HWaddr 02:00:00:00:00:00  
          inet addr:172.16.0.2  Bcast:172.16.255.255  Mask:255.255.0.0
STM: App open(/proc/net/if_inet6) = (fd:-2)          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2 errors:0 dropped:2 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)
```

- ping HostOS to check the network status

```shell
/ # ping 172.16.0.1
PING 172.16.0.1 (172.16.0.1): 56 data bytes
64 bytes from 172.16.0.1: seq=0 ttl=64 time=1.609 ms

--- 172.16.0.1 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max = 1.609/1.609/1.609 ms

- Starting another Arrow Busybox Instance in another terminal
``` shell
$ sudo ./bin/actrl shoot -t busybox sh
```

- Using below commands to attach the Busybox Instance's STDIO with your terminal's

``` shell
$ sudo ./bin/actrl attach
```

- Using below command to check the network status in Busybox shell

``` shell
/ # ifconfig
eth0      Link encap:Ethernet  HWaddr 02:00:00:00:00:01  
          inet addr:172.16.0.3  Bcast:172.16.255.255  Mask:255.255.0.0
```

- Ping the first Arrow Busybox Instance we started whose IP address should be 172.16.0.2
```
/# ping 172.16.0.2
```
Here you can find that Arrow Instances are connected through Standard TCP/IP Network through Linux bridge. 

Arrow Single Task kernel is based on standard upstream Linux, you can use Busybox Instance to explore this Single Task Kernel through /Proc, /Sys, check kernel message using command dmesg.

