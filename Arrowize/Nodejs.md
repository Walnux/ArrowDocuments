# Run Node.js Applications on Arrow

[Overview](#overview)


[Try Node.js Arrow Meta](#try-nodejs-arrow-meta)

[Run Node-hello on Arrow](#run-node-hello-application-on-arrow)

[Run Chat Service on Arrow](#run-chat-service-on-arrow)

[Using Express-photo-gallery module to develop and run gallery service on Arrow](#using-express-photo-gallery-module-to-develop-and-run-gallery-service-on-arrow)
## Overview
Node.js is an open-source, cross-platform, JavaScript runtime environment. It executes JavaScript code outside of a browser. For more information on using Node.js, see the Node.js Website.

In Arrow 0.1 release, the Node.js support for Arrow has been added. Node.js v12.4.0 runtime binary is compiled and statically linked by ASDK, and be put into Node.js Arrow Binary for Node.js applications to use. Node.js Arrow application is packeted as Node.js Application/Microservice Arrow Image which includes user's JavaScript and the third party modules it depends on. Arrow supports third party Node.js module and the modules manage tool npm well. See [Arrow System Working Mode](https://github.com/Walnux/ArrowDocuments/blob/master/ArrowWorkingMode.md)

Run Node.js Applications according to steps below.

## How to Run Node.js Applications on Arrow
After [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd) is installed. Node.js Arrow Binary, [Node Arrow Meta](https://github.com/Walnux/ameta/tree/master/node) and Node.js sample application [node-hello](https://github.com/Walnux/ameta/tree/master/node-hello) has been preinstalled in the development machine. 

### Try Nodejs Arrow Meta 

Notes: In Arrow 0.1 release, run below commands under Arrow Service source directory, which is located at $HOME/go/src/github.com/Walnux/arrowd. 

``` shell 

$ sudo ./bin/actrl shoot node 

$ sudo ./bin/actrl logs

... 
v12.4.0
...
``` 

Notes: In Arrow 0.1 release Node Arrow Meta is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/ameta/node  

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

### Run node-hello application on Arrow

node-hello is the service to inform current date, time and timezone from http server. 

``` shell 

$ sudo ./bin/actrl shoot node-hello 
``` 

Notes: node-hello Arrow Image is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/ameta/node-hello  

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

Arrow Binary node-v12.4.0 is used and command: "node hello.js" is run when shooting node-hello. node-hello service is serving on port 3003, and the service is exported from port 3003.The service can be accessed through http://localhost:3003. on host machine.

Using web browser to access the service. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/NodeHello.jpg"> 

</p> 

### Run Chat Service on Arrow

[feathers-chat](https://github.com/feathersjs/feathers-chat) uses Feathers, a framework for real-time applications and REST APIs. It contains the chat service created in the Feathers guide and a frontend in plain JavaScript. Feather-chat can be run very easily on Arrow. 

``` shell
$ sudo make asdk
/ # cd /admeta

/ # git clone https://github.com/feathersjs/feathers-chat.git
/ # cd feathers-chat
/ # npm install
```

Notes: If npm is not installed in the ASDK, using below command to install npm. 

``` shell
/ # apk add npm
```

create below arrow_spec.json in /admeta/feathers-chat
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
			"src/"
		]
	},
	
	"port": 3030,
	"export": 3030,
	"proto": "tcp"
}
``` 
Notes: ASDK directory /admeta is bound with Arrow Meta on development machine, which is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/ameta

Now feathers-chat is ready to shoot. Exit from ASDK and shoot features using below commands.

```shell
/ # exit

$ sudo ./bin/actrl shoot feathers-chat 
$ sudo ./bin/actrl logs 
... 
info: Feathers application started on http://localhost:3030 
```

Node.js Arrow Binary is used by service feathers-chat; When shooting feathers-chat, command: node /src is run; this chatting service is serving on port 3030, and the service is exported from port 3030.The service can be accessed through http://localhost:3030. on host machine.

Using web browser to access the chatting service. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/feathers-chat-login.jpg"> 

</p> 
<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/feathers-chat.jpg"> 

</p> 

### Using Express-photo-gallery Module to develop and run gallery service on Arrow

Arrow supports third party Node.js module as well as the modules managing tool npm very well. [express-photo-gallery Module](https://www.npmjs.com/package/express-photo-gallery) is a node module that creates an Express.js middleware function for hosting stylish and responsive photo galleries using jQuery lightgallery. In this example, EPG is used to develop and run a gallery service on Arrow.

Please follow below steps to develop gallery service on ASDK.

``` shell
$ sudo make asdk
/ # mkdir /admeta/gallery
/ # cd /admeta/gallery 
/ # npm install express-photo-gallery
```

Notes: If npm is not installed in the ASDK, using below command to install npm 

``` shell
/ # apk add npm
```

create file app.js in /admeta/gallery

``` js
var express = require('express');
var app = express();

var Gallery = require('express-photo-gallery');

var options = {
  title: 'My Awesome Photo Gallery'
};

app.use('/photos', Gallery('photos/', options));

app.listen(3001);
```

create file arrow_spec.json in /admeta/gallery
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
			"app.js"
		]
	},
	
	"port": 3001,
	"export": 3008,
	"proto": "tcp"
}
``` 
Now, it is time to prepare the photos for the gallery service.

After putting the photos in directory /admeta/gallery/photos of ASDK, using steps below to create the thumbnails for the photos for the gallery service.

``` shell
/ # apk add imagemagick
/ # apk add graphicsmagick
/ # npm install -g epg-prep
/# epg-prep /admeta/gallery/photos
```
Notes: ASDK directory /admeta is bound with Arrow Meta on development machine, which is located at: $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/ameta

Now gallery service is ready to shoot. Exit from ASDK and using below commands to shoot.

```shell
/ # exit

$ sudo ./bin/actrl shoot gallery 
```

Node.js Arrow Binary is used by service gallery; When shooting gallery service, command: node app.js is run; this gallery service is serving on port 3001, and the service is exported from port 3008.The service can be accessed through http://localhost:3008 on the host machine.

Using web browser to access the gallery service. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/PhotoGallery.jpg"> 

</p> 


## Understanding [Arrow System Working Mode](https://github.com/Walnux/ArrowDocuments/blob/master/ArrowWorkingMode.md)
From above examples, it is easy to understand Arrow System Working Mode. The developers who use Node.js-12.4.0 to develop the microservices only need to care about his/her own applications and don't have to package the application with Node.js runtime or any base OS, tools and so on. User only needs to specify what Arrow Binary will being used in arrow_spec.json file.
