# Run Node.js Applications on Arrow

## Node.js overview
Node.js is an open-source, cross-platform, JavaScript runtime environment. It executes JavaScript code outside of a browser. For more information on using Node.js, see the Node.js Website.
## Arrow and Nodejs
In current Arrow 0.1 release, the Node.js support for Arrow has been added. Node.js v12.4.0 runtime binary is compiled and statically linked by ASDK, and be put into Node.js Arrow Binary for Node.js applications to use. Node.js Arrow application is packed as Node.js Application/Microservice Arrow Image which includes user's JavaScript and the third party modules it depends on. These modules are managed by npm.

Run Node.js Applications according to steps below.

## How to Run Node.js Applications on Arrow
After [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd) is installed. Node.js Arrow Binary, [Node Arrow Meta](https://github.com/Walnux/ameta/tree/master/node) and Node.js sample application [node-hello](https://github.com/Walnux/ameta/tree/master/node_hello) has been preinstalled in the developing machine. 

- Try Node.js Arrow Meta 

Notes: In Arrow 0.1 Prove of Concept release, run below command under Arrow Service source directory. Arrow Service source directory is located $HOME/go/src/github.com/Walnux/arrowd. 

``` shell 

$ sudo ./bin/actrl shoot node 

$ sudo ./bin/actrl logs

... 
v12.4.0
...
``` 

Notes: Node Arrow Meta is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/meta/node  

Have a look at file node/arrow_spec.json in the directory 

``` json 
{
	"binary": {
		"name": "node",
		"version": "v12.4.0",
		"project": "https://github.com/nodejs/node.git"
	},

	"process": {
		"terminal": false,
		"cmd": "node",
		"args": [
			"node",
			"--version"
		]
	}

}
``` 

Arrow Binary node-v12.4.0 is used and command: "node –version" is run when shooting node. 

User can use Node Arrow Meta as template to run his/her own application very easily. 

- Run node-hello application on Arrow

node-hello is the service to report the current date, time and timezone through http. 

``` shell 

$ sudo ./bin/actrl shoot node-hello 
``` 

Notes: Node Arrow Meta is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/meta/node  

Have a look at file node-hello/arrow_spec.json in the directory 

``` json 
{
	"binary": {
		"name": "node",
		"version": "v12.4.0",
		"project": "https://github.com/nodejs/node.git"
	},

	"process": {
		"terminal": false,
		"cmd": "node",
		"args": [
			"node",
			"hello.js"
		]
	},

	"port": 3003,
	"export": 3003,
	"proto": "tcp"
}
``` 

Arrow Binary node-v12.4.0 is used and command: "node hello.js" is run when shooting node. node-hello service is serving on port 3003, and the service is exported from port 3003.The service can be accessed through http://localhost:3008. on host machine.

Using web browser to access the service. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/NodeHello.jpg"> 

</p> 

- run [feathers-chat](https://github.com/feathersjs/feathers-chat) on Arrow

Feather-chat uses Feathers, a framework for real-time applications and REST APIs. It contains the chat application created in the Feathers guide and a frontend in plain JavaScript. It can run easily on Arrow. 

``` shell 
$ sudo make asdk
#cd /admeta

#git clone https://github.com/feathersjs/feathers-chat.git
#cd feathers-chat
#npm install
```

create below arrow-spec.json in /admeta/feathers-chat
``` json
{
	"binary": {
		"name": "node",
		"version": "v12.4.0",
		"project": "https://github.com/nodejs/node.git"
	},

	"process": {
		"terminal": true,
		"cmd": "node",
		"args": [
			"node",
			"src/"
		]
	},
	
	"port": 3030,
	"export": 3030,
	"proto": "tcp"
}
``` 
Notes: ASDK directory /admeta is bound with Host Machice Arrow Meta which is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/meta

Now feathers-chat is ready to shoot.

```shell
#exit

$ sudo ./bin/actrl shoot feathers-chat 
$ sudo ./bin/actrl logs 
... 
info: Feathers application started on http://localhost:3030 
```

Node.js Arrow Binary is used by service feathers-chat; When shooting feathers-chat, command: node /src is run; the chat service is serving on port 3030, and the service is exported from port 3030.The server can be accessed through http://localhost:3030. on host machine.

Using web browser to access the chat service. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/feathers-chat-login.jpg"> 

</p> 
<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/feathers-chat.jpg"> 

</p> 

## understand [Arrow System Working Mode](https://github.com/Walnux/ArrowDocuments/blob/master/ArrowWorkingMode.md)
From above examples, it is easy to understand Arrow System Working Mode. 
