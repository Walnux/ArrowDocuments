# Run Nginx on Arrow

## Arrow and Nginx
[Nginx](https://www.nginx.com/) is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

In Arrow 0.1 Release. Nginx has been integrated into [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and pre-installed in the development machine. It can be run on Arrow using [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md) very easily. 

## How to Run Nginx on Arrow
- After setting up [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). And Arrow Service has been started properly.

Notes: In Arrow 0.1 release, please make sure run Nginx in Arrow Service source directory, which is located at $HOME/go/src/github.com/Walnux/arrowd on the development machine. 

```shell
$ sudo ./bin/actrl shoot nginx
```

- Using wget to acess the nginx based http server

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
