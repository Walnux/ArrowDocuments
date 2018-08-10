# arrow User Manual
arrow is the command line client of arrowd service. It can be used to use Arrow

## arrow run
```
$ crossbow run [OPTIONS] ArrowImage[:TAG] [COMMAND] [ARG...] [--] [ENV1=env1_value ENV2=env2_value...]
```

### Detached vs foreground
When running an Arrow image, you must first decide if you want to run the arrow in the background in a “detached” mode or in the default foreground mode
```
-d=false: Detached mode: Run Arrow in the background, print new Arrow id
```

> Note: ` -d=false ` means the attached foregroud mode is the default setting if you do not add ` -d ` or ` -d=true `

In foreground mode, ` crossbow run ` can start Arrow image and attach the console to the process’s standard input, output, and standard error. It can even pretend to be a TTY which is most command line executables expect.

> Note: Since Arrowized application runs as PID 1, it ignores any signal with the default action. so Arrowized application will not terminate on SIGINT or SIGTERM unless the application coded to do so. The [Arrowized busybox](/link/to/Arrowized_Busybox.md) shell will never exit with the two singles, while The [Arrowized Nodejs](/link/to/Arrowwized_Nodejs.md) commanline will exit with 2 continue ^c.

### ArrowImage[:tag]
While not strictly a means of identifying a Arrow image, you can specify a version of an Arrow image you’d like to run the Arrow image by adding ArrowImage[:tag] to the command. For example, ` crossbow run node:10.6.0 `.

### Network settings
```
--dns=[]           : Set custom dns servers for the Arrow
--network="bridge" : Connect the Arrow into a network
                      'bridge': create a network stack on the default Arrow bridge
                      'none': no networking
                      'bridge-name': connect to a existing bridge
--ip/mask=""       : Sets the Arrow's Ethernet device's IPv4 address and subnet mask
--gateway=""       : Set the Arrow's Ethernet device's gateway address
--mac-address=""   : Sets the Arrow's Ethernet device's MAC address
--hostname=""      : Set the Arrow's Host name
```
If you Arrowize your applications with Networking support, by default all Arrows have networking enabled and they can make any outgoing connections. The operator can completely disable networking with ` crossbow run --network none ` which disables all incoming and outgoing networking. In cases like this, you would perform I/O through files or STDIN and STDOUT only. Networking settings to Arrowized application without Networking support will be ignored.


> Note: In order to use networking, you must have networking supporting in your Arrowized applications. So the Arrow kernel image with networking support must be used to arrowize your applications. [see Arrowize your applications](/path/to/Arrowize_Application.md)  

By default, the MAC address, hostname and gateway are generated basing on the IP address allocated to the Arrow. You can set the Arrow’s MAC address explicitly by providing a MAC address via the --mac-address parameter (format:12:34:56:78:9a:bc).Be aware that Arrow network does not check if manually specified MAC addresses are unique.

Supported networks :

| Network           | Description                                              |
| ----------------- | -------------------------------------------------------- |
| none              | No networking in the Arrow.                          |
| bridge (default)	| Connect the Arrow to the bridge created by Arrow service via tun/tap interfaces. |
| bridge_name	      | Connect the Arrow to the existing bridge       |

[Arrow network](/path/to/Arrow_Network.md) is based on Linux bridge, Arrow will use tun/tap to connect to the Host bridge. if ` --network="bridge" ` is set, the Arrow bridge created by Arrow (daemon) service will be used, and ` --ip/mask --gateway ` can be assigned automatically. if ` --network="bridge_name" ` is set the existing bridge on host named as ` bridge_name ` will be used. At this situation, normally you need to set --ip/mask --gateway manually. You can use this method to add Arrow into the container network and commuicate with the containers in the the network.

### Volume setting --volume="ArrowPath@HostPath, ArrowPath@HostPath, ..."
- **HostPath** path at host share with Arrow
- **ArrowPath** path at Arrow share the **HostPath**

Currently, only the P9 based Volume share are supported.

The readonly metadata Volume support will be supported in the future.

also see [Arrow Filesystem](https://github.com/Walnux/Arrow_Documents/blob/master/Design/ArrowFilesystem.md)

### Example
` #crossbow run --network=none hello_arrow hello_world `

Run application hello_world on arrowized hello_world Arrow image, without network support in foreground mode.

` #crossbow run busybox_arrow sh `

Run command sh on Arrow image busybox_arrow in foreground mode. see [Arrowize Busybox](https://github.com/Walnux/Arrow_Documents/blob/master/Arrowize/ArrowizeBusybox.md)

` #crossbow run node_arrow node -- NODE_DEBUG=* NODE_DEBUG_NATIVE=http2 `

Run command node on Arrow image node_arrow in foreground mode, the environment parameter NODE_DEBUG set as * means debug all the node modules, NODE_DEBUG_NATIVE set as http2 means debug native C++ http2 module.

` #crossbow run -d --volume="/var@/home/martin/node_js" node_arrow node /var/my_http_server.js -- NODE_DEBUG=* `

This command will start up a nodejs https server in background. The java script file my_http_server should in /home/martin/node_js directory, the directory will be mounted to Arrow filesystem /var. Environment paramter NODE_DEBUG is set as * means all the node nodules will be debuged and the debug information will be printed out. By default, it will use Arrow network configure automatically setting by Arrow system.   

## crossbow ps
### Description
List running Arrows

### Usage
crossbow ps

### example

```
$ crossbow ps
ARROW ID        IMAGE                COMMAND      STATUS         
4c01db0b339c    hello_world          hello        Up 16 seconds
d7886598dbe2    busybox              sh           Up 33 minutes
```
## crossbow inspect
### Description
Return detailed information about the specific Arrow 

### Usage
crossbow inspect ID/NAME [ID/NAME...]

### example
```
$ crossbow inspect 4c01db0b339c
/* ToDo: Add example */
```
### crossbow attach
### Description
Attach local standard input, output, and error streams to a running Arrow


### Usage
crossbow attach ID/NAME

### Extended description
Use crossbow attach to attach your terminal’s standard input, output, and error (or any combination of the three) to a running Arrow using the Arrow’s ID or name. This allows you to view its ongoing output or to control it interactively, as though the commands were running directly in your terminal.

> Note: The attach command will display the output of the ENTRYPOINT/CMD process. This can appear as if the attach command is hung when in fact the process may simply not be interacting with the terminal at that time.

You can attach to the same contained process multiple times simultaneously, from different sessions on the host.

> Note: Since Arrow is running as PID 1 it ignores any signal with the default action. So, the process will not terminate on SIGINT or SIGTERM unless it is coded to do so.
```
/* ToDo: Need to figure out */
It is forbidden to redirect the standard input of a cross attach command while attaching to a tty-enabled Arrow (i.e.: launched with -t).
```
While a client is connected to Arrow’s stdio using crossbow attach, Arrow uses a ~1MB memory buffer to maximize the throughput of the application just like what docker does. If this buffer is filled, the speed of the API connection will start to have an effect on the process output writing speed. This is similar to other applications like SSH. Because of this, it is not recommended to run performance critical applications that generate a lot of output in the foreground over a slow client connection. Instead, users should use the crossbow logs command to get access to the logs.

### Example

```
$ crossbow run -d --name node_inter Arrow_node node

$ crossbow attach node_inter
# help
/* ToDo: Add example*/
```
## crossbow logs
# Description
get the logs of the Arrow
/* ToDo Needs to figure out */


## crossbow kill
### Description
Kill one or more running Arrows

### Usage
crossbow kill CONTAINER [CONTAINER...]
### Extended description
/* ToDo Needs to figure out */
The docker kill subcommand kills one or more containers. The main process inside the container is sent SIGKILL signal (default), or the signal that is specified with the --signal option. You can kill a container using the container’s ID, ID-prefix, or name.

Note: ENTRYPOINT and CMD in the shell form run as a subcommand of /bin/sh -c, which does not pass signals. This means that the executable is not the container’s PID 1 and does not receive Unix signals.

### Examples
/* ToDo: Add example */

Note: This docuemnts referece [Docker manual](https://docs.docker.com/engine/reference/commandline/docker/)``` 
