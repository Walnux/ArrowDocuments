# Run Nginx on Arrow
[Overview](#overview)

[Try Nginx Arrow Meta](#try-nginx-arrow-meta)

[Run Home Page Service on Arrow](#run-home-page-service-on-arrow)


## Overview
[Nginx](https://www.nginx.com/) is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

In Arrow 0.1 Release. Nginx has been integrated into [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and pre-installed in the development machine. It can be run on Arrow using [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md) very easily. 

## Try Nginx Arrow Meta
After setting up [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). And Arrow Service has been started properly.

Notes: In Arrow 0.1 release, please make sure run Nginx in Arrow Service source directory, which is located at $HOME/go/src/github.com/Walnux/arrowd on the development machine. 

Use below command to try Nginx Arrow Meta

```shell
$ sudo ./bin/actrl shoot nginx
```

Using wget to acess the nginx based http server

``` shell
$ wget localhost
--2020-10-15 19:38:36--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 171 [text/html]
Saving to: ‘index.html’

index.html
100%[================================================================================================================>]     171  --.-KB/s    in 0.001s  

2020-10-15 19:38:36 (289 KB/s) - ‘index.html’ saved [171/171]
```

## Run Home Page Service on Arrow
home-page service is preinstalled in the development machine by ASDK. This service is a http web server serving Arrow home page. Use below command to start the service.

``` shell
$ sudo ./bin/actrl shoot home-page
```
check home-page application Arrow Image in $HOME/go/src/github.com/Walnux/arrowd/.work/var/arrowd/pieces/ameta/home-page
from file arrow_spec.json
``` json 
{
	"binary": {
		"name": "nginx",
		"version": "1.7.12",
		"project": "nginx"
	},

	"process": {
		"terminal": false,
		"cmd": "nginx",
		"args": ["nginx"]
	},

	"port": 80,
	"export": 3006,
	"proto": "tcp"
}
```
- The service is exported from port 3006. Access the service on http://localhost:3006.

- The static html pages is located at html directory. 

- Directory conf contains the configuration files to run Nginx Arrow Binary.
