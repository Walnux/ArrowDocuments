# Run Busybox On Arrow

[Overview](#overview)

[Start Arrow Shell Environment](#start-arrow-shell-environment)

[Checking Network Configuration in Arrow Shell Environment](#checking-network-configuration-in-arrow-shell-environment)

[Run Busybox Command Outside of Arrow Shell Environment](#run-busybox-command-outside-of-arrow-shell-environment)

[Debug Arrow Single Task Kernel in Arrow Shell Environment](#debug-arrow-single-task-kernel-in-arrow-shell-environment)

## Overview
Busybox is the true Swiss Army Knife of Embedded Linux. It integrates nearly all the general linux features/tools into one binary, and identify the feature user want to use through link name. the link name will be saved at argv[0] as the command name. Arrow populate the argv[0] with command name. That is compatible with Busybox design.

In Arrow 0.1 Release. Busybox has been integrated into [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK). You can use ASDK to build "Combined Mode" Busybox Arrow Binary and run it through [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). 

In Arrow, Busybox is only used to debug Arrow Single Task Kernel and will not be packaged with the application. Busybox based Arrow Shell environment provides the standard Linux Shell using experience.

Using below steps to try Arrow Shell Environment.


## Start Arrow Shell Environment
After setting up [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). And Arrowd has been started. You can run Busybox based shell environment on Arrow in Arrow Service source directory:

Notes: Arrow Service source directory is $HOME/go/src/github.com/Walnux/arrowd. 

```shell
$ sudo ./bin/actrl shoot -t busybox sh
```

Using below command to check shell running status
``` shell
$ sudo ./bin/actrl list
busybox bpfaeddd5h2u8e3q7svg    sh      sh      io.arrowd.arrow.status.running.v1
```

Using below command to enter Arrow Shell Environment.

``` shell
sudo ./bin/actrl attach
```

## Checking Network Configuration in Arrow Shell Environment  

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

- Run one more Arrow Shell Enironment in another terminal on the development machine

``` shell
$ sudo ./bin/actrl shoot -t busybox sh
```
- Entering the Shell Enviornmnet
``` shell
$ sudo ./bin/actrl attach
```

- Check the network status in this Arrow shell Environment
``` shell
/ # ifconfig
eth0      Link encap:Ethernet  HWaddr 02:00:00:00:00:01  
          inet addr:172.16.0.3  Bcast:172.16.255.255  Mask:255.255.0.0
```
- Ping the first Arrow shell Envionment
```shell
/ # ping 172.16.0.2
```
The two Arrow shell Enviornment is connected with each other.

- Using below command to exit the Busybox

``` shell
/ # exit
```

## Run Busybox Command Outside of Arrow Shell Environment
Running Busybox Command outside of Arrow Shell environment is also allowed. When running out side of Shell environment, The Busybox Arrow Binary is used to run the related command. It is as easy as running a normal native application.

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

``` shell
$ sudo ./bin/actrl shoot busybox ping 172.16.0.2
```

- Using logs command to check the result

``` shell
$ sudo ./bin/actrl logs
```
According to above result, All the shot Arrows are properly configured and connected through Standard TCP/IP Network. 

## Debug Arrow Single Task Kernel in Arrow Shell Environment
Arrow Single Task Kernel is based on the standard Linux Kernel, you can use Busybox Shell to explore this Single Task Kernel through /Proc and /Sys filesystem, check Kernel message using dmesg, like on standard Linux Shell Environment.

## Next Step
[Run Nginx on Arrow](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/Nginx.md)
