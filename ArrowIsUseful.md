# Moden cloud needs a simple, secure, low latency and low overhead way to run software

## Cloud is obese, slow and not secure enough

Cloud Computing can be simply understood as packages of users' software running on the [Cloud Infrastructure](https://en.wikipedia.org/wiki/Infrastructure_as_a_service).

We know most of the software running on the cloud evolved from Personal Computer(PC) and Physical Server era. They run in the full feature Operating System (OS) like Ubuntu which includes OS Kernel, libraries, tools, OS system services, middleware and so on. So in order to run the software on cloud, they have to be packaged with the full feature OS and deployed onto cloud. We call this [System Central Solution](/TopDown.md)

In order to deploy, run, manage and orchestrate these heavy packages, big amount of cloud resources are needed. However, In most situation, software only use part of the resources. A lot of resources are actually wasted.

The big size of software package is the main reason why cloud is slow. 

Besides, the redundant components in the package expose a lot of attack interfaces which can be exploited by the malicious software. The complicated full feature OS inherited from old era may also inherit the old security holes. The extra resources can also be used by the malicious software to enforce the attacking easily. The obesity increases the cloud security risk.

This expensive, slow and unsafe way to run software on cloud can't meet the development of the modern cloud. 

## The trends of modern cloud
Cloud era brought revolution of computerization world. This revolution created a huge and fast growing market<sup>[1](https://www.statista.com/statistics/510350/worldwide-public-cloud-computing/)</sup>.

Traditional Cloud [Infrastuctre as a Service (IaaS)](https://en.wikipedia.org/wiki/Infrastructure_as_a_service) liberates individuals and orgnizations from the burden to maintain their physical servers and infrastrucre on premise.

Cloud market and technology innovations are just begin. what are the trends of the moden cloud?

- [Serverless computing](https://en.wikipedia.org/wiki/Serverless_computing) will liberate cloud users from maintaining the complicated virtual servers and cloud infrastructure. People can just focus on their own tasks that really matter their business. The global serverless architecture market size is expected to reach USD 19.84 billionby 2025 at a 26.0% CAGR during the forecast period, according to a new study by Grand View Research, Inc.<sup>[4]</sup>

- CSP Edge Computing extends computing resources from cloud to users' premise where the data are created. It bridges the Internet of Things (IoT) with Cloud, and will greatly promote the booming of IoT and Cloud market. The global edge computing market size is expected to reach USD 28.84 billion by 2025 registering a CAGR of 54.0%, according to a new report by Grand View Research, Inc.[?](https://www.grandviewresearch.com/press-release/global-edge-computing-market)


to meet the reqirements of Serverless, unified Cloud Edge Computing and IoT, security is still the top priority, low latency and low overhead to run sofware become more and more critical.    

## We need a way to simply and securly run software with low latency and low overhead on moden cloud and edge computing   
While in moden cloud where serverless computing technoloies will widely used by CSP Edge Computing, the applications and software used to construct the user defined serverless framework may flow from Cloud to edge and run instantly to reponse the events or handle the data on variable of usage case with very low latency.  

At same time, security is always the top priority. Applications and software should be run in secure and isloated environemnt, in case the untrusted sofware impact other part of the system.  

Becuase of the restricted resources on IoT and Edge side, the software should be run with very low overhead.

Furthmore the tranditaional cloud usage like [LAMP backed website]() also needs a simle and secure way to run sofware with low overhead, that will make the whole cloud more slim and effienecy.

Virtual Mahine Image workload technology leads us to the Cloud era. It made it possible to deploy and run the cusotmers' server images (inlcuding the whole operation system an software stack ) on virtual server.

Now We need an innovation which can just simply and securly run software on cloud with low latency and overhead. And It may lead us to another revlution in moden cloud.

## Industrial is waiting for a safe simple agile and low overhead workload to push cloud forward

Currently, the main workload in cloud is traditional full feature Virtual Machine with the full feature guest OS, middlewares and libraris to run applications. It is very redundant and slow. And the overall infrastrucure is also quite complicated. 

Recent years, Container like Docker comes to dominate the cloud workload. Containers can be used to package, ship and run the software isolated directly on the hostOS. Containers share the same kernel which greatly increases the code running indensity and efficiency. But container is not sandbox. Security and stability is a problem. Besides Container like docker container implementaion is very complicated . And not easy to be used at some resource limtted edge computing environemnt or some FaaS solution directly like AWS Greengrass. Furthermore, although Docker Container can be used to package single application, most people still tend to use it to package the whole system ever running on the virtual Machine. That is one of the reason why docker container suceed. But it can't help the whole cloud and edge ecosystem small and simple.

Arrow shares some basic views with Unikernel like run single application on Virutal Machine. But Arrow is actually differnt solution with Unikernel. Unikernel is the libOS which link application with the specific OS libearis and run on VM. While Arrow makes use of existing mature Linux Kernel. And Application runs on the standarnd Linux environment. So Arrow can make full use of exising Linux resources. Most importantly most of these resources are well verified and safe enough for Arrow to reach the production quality.

However, Arrow can't do everything. It can't be used to package the whole OS system. Arrow System can be think of part of hostOS or cloud infrastrucre to package and run sigle application. With Arrow System, users do not need to package and ship their own software, instead they only need to ask Arrow System to run some specific applications as Arrows to compose and fullfill their specific goal.     

[1] [Total size of the public cloud computing market from 2008 to 2020](https://www.statista.com/statistics/510350/worldwide-public-cloud-computing/)
[2] [Infrastrutur as a Service (IaaS)](https://en.wikipedia.org/wiki/Infrastructure_as_a_service)
[4] https://www.grandviewresearch.com/press-release/global-serverless-architecture-market
The worldwide infrastructure as a service (IaaS) market grew 31.3% in 2018 to total $32.4 billion, up from $24.7 billion in 2017, according to Gartner, Inc. <sup>[2](https://www.statista.com/statistics/510350/worldwide-public-cloud-computing/)</sup>


in now days, Cloud is developing into Serverless era. At same time Unified Cloud and Edge Computing solution which binds Interneter of Things (IoT) with Cloud computing will greately promote the IoT and Cloud market.

