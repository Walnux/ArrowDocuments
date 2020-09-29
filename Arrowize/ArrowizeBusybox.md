# Running Busybox as Arrow Instance

## Arrow and Busybox
Busybox is the true Swiss Army Knife of Embedded Linux. It integrates nearly all the general linux features/tools into one binary, and identify the feature user want to use through link name. the link name will be saved at argv[0] as the command name. Arrow populate the argv[0] with command name. That is compatible with Busybox design.

Busybox is the ideal tool to debug Arrow Single Task Kernel. Running Busybox as Arrow Instance, actually, you might be using the normal Linux.

In Arrow 0.1 Release. Busybox has been integrated into [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK). You can use ASDK to build "Combined Mode" Busybox Arrow Binary and run it as Arrow Instance through [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). 

## How to Run Busybox as Arrow Instance
- After setting up [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). And Arrowd has been started. You can run Busybox Binary as Arrow Instance in Arrowd source directory:

Notes: In Arrow 0.1, please make sure you are in Arrow Service source directory to run below command. Normally Arrow Service source directory is $HOME/go/src/github.com/Walnux/arrowd. 

```shell
$ sudo ./bin/actrl shoot -t busybox sh
```

- Using below command to check the Arrow Instance running status
``` shell
$ sudo ./bin/actrl list
busybox bpfaeddd5h2u8e3q7svg    sh      sh      io.arrowd.arrow.status.running.v1
```

- Using below command to enter the Single Task Kernel Shell Environment. It is actually a compact Linux Shell environment

notes: it actuallly attach Busybox Arrow Instance STDIO with current terminal
``` shell
sudo ./bin/actrl attach

/ # ls
data  dev   etc   proc  root  sys   tmp
```

- Using ifconfig command to check the network configuration

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
```

- Starting one more Busybox Instance in another terminal

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

- Using below command to exit the Busybox

``` shell
/ # exit
```

- Directly running the related command outside of Shell environment is also allowed. When running out side of Shell environment, Busybox Arrow Instance is started to run the related command and save the STDOUT into the logger file then exits. It is as easy as running a normal native application.

``` shell
$ sudo ./bin/actrl shoot busybox ping 172.16.0.1
```

- Using logs command to show the result

```
$ sudo ./bin/actrl logs

PING 172.16.0.1 (172.16.0.1): 56 data bytes
64 bytes from 172.16.0.1: seq=0 ttl=64 time=0.293 ms
clocksource: tsc: mask: 0xffffffffffffffff max_cycles: 0x2717868ea45, max_idle_ns: 440795316085 ns
64 bytes from 172.16.0.1: seq=1 ttl=64 time=0.466 ms
64 bytes from 172.16.0.1: seq=2 ttl=64 time=0.491 ms
random: fast init done
64 bytes from 172.16.0.1: seq=3 ttl=64 time=0.557 ms
64 bytes from 172.16.0.1: seq=4 ttl=64 time=0.533 ms

--- 172.16.0.1 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.293/0.468/0.557 ms
```

- Ping the first Arrow Busybox Instance whose IP address is 172.16.0.2
```
/# ping 172.16.0.2
```

According to above result, Arrow Instances are properly configured and connected through Standard TCP/IP Network. 

Arrow Single Task Kernel is based on the standard Linux Kernel, you can use Busybox Instance to explore this Single Task Kernel through /Proc and /Sys filesystem, check Kernel message using dmesg.

## Next Step
[Run Nginx Arrow Instance](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nginx.md)
