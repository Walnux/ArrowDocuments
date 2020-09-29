# Running Nginx as Arrow Instance

## Arrow and Nginx
[Nginx](https://www.nginx.com/) is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache.

In Arrow 0.1 Release. Nginx has been integrated into [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK). You can use ASDK to build "Combined Mode" Nginx Arrow Binary Arrow Meta and run it as Arrow Instance through [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). 

## How to Run Nginx as Arrow Instance
- After setting up [ASDK](https://github.com/Walnux/Atools/tree/master/ASDK) and [Arrow Service](https://github.com/Walnux/arrowd/blob/master/README.md). And Arrowd has been started. You can run Nginx as Arrow Instance in Arrowd source directory:

Notes: In Arrow 0.1 release, please make sure you are in Arrow Service source directory to run below command. Normally Arrow Service source directory is $HOME/go/src/github.com/Walnux/arrowd. 

```shell
$ sudo ./bin/actrl shoot nginx nginx
```

- Using wget to check the nginx server status

``` shell
$ wget 172.16.0.5
--2020-06-08 17:03:15--  http://172.16.0.5/
Connecting to 172.16.0.5:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1828 (1.8K) [text/html]
Saving to: ‘index.html.8’
2020-06-08 17:03:15 (109 MB/s) - ‘index.html.8’ saved [1828/1828]
```

- Using below command to export http service
``` shell
$ sudo ./bin/actrl shoot -p 80:80/tcp nginx nginx
```

- Access the http service from the other node connected with the hostnode where Arrow system is running
``` shell
$ wget 10.0.0.90
--2020-06-08 10:11:42--  http://10.0.0.90/
Connecting to 10.0.0.90:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1828 (1.8K) [text/html]
Saving to: ‘index.html.7’

2020-06-08 10:11:42 (115 MB/s) - ‘index.html.7’ saved [1828/1828]

```

Note 10.0.0.90 is the IP address of host where Arrow system is running.
