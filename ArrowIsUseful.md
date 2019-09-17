# users are waiting for a safe simple swift and low overhead way to run software on moden cloud

Cloud brought a revolution to the internet, and it is still evolving very quickly, what is the next revolution?

Cloud technology liberates individuals and orgnizations from the heavy burden to maintain their physical servers on premise, instead, people just rent the Virtual Machines to build their servers from The Cloud Service Providors. At the same time, the central manangement and dispatchemnt of server computing, networking and storage resouces greatly promots the efficency to use these resources. This revolution created a huge and still fast growing market. [According to the Stamford, Connecticut-based research firm, the worldwide infrastructure as a service (IaaS) market grew 31.3% in 2018 reaching $32.4 billion, up from $24.7 billion in 2017.](https://www.forbes.com/sites/jeanbaptiste/2019/08/02/amazon-owns-nearly-half-of-the-public-cloud-infrastructure-market-worth-over-32-billion-report/#7eb2280f29e0)

Cloud technology keeps evolving. Then, what is the future of Cloud?
Let's start from the motivation behind the huge investment on the physical or virtual servers. Obviosly, people want to run applications on these servers to provide some kind of services through Internet like the widely used webserver or to reponse or handle some events instantly like AWS Lambda.

However, In order to run these applications, people still have to install and maintain the full software stack on the full feature server. No matter the server is physical or viturial. It is the big burden for user. and a lot of cloud resources are wasted. Becuase the application only use part of the software and hardware resources on the server.

Could we just run the application and don't have to care about the server anymore? That is call Serverless - the future of Cloud.



Currently, the main workload in cloud is traditional full feature Virtual Machine with the full feature guest OS, middlewares and libraris to run applications. It is very redundant and slow. And the overall infrastrucure is also quite complicated. 

Recent years, Container like Docker comes to dominate the cloud workload. Containers can be used to package, ship and run the software isolated directly on the hostOS. Containers share the same kernel which greatly increases the code running indensity and efficiency. But container is not sandbox. Security and stability is a problem. Besides Container like docker container implementaion is very complicated . And not easy to be used at some resource limtted edge computing environemnt or some FaaS solution directly like AWS Greengrass. Furthermore, although Docker Container can be used to package single application, most people still tend to use it to package the whole system ever running on the virtual Machine. That is one of the reason why docker container suceed. But it can't help the whole cloud and edge ecosystem small and simple.

Arrow shares some basic views with Unikernel like run single application on Virutal Machine. But Arrow is actually differnt solution with Unikernel. Unikernel is the libOS which link application with the specific OS libearis and run on VM. While Arrow makes use of existing mature Linux Kernel. And Application runs on the standarnd Linux environment. So Arrow can make full use of exising Linux resources. Most importantly most of these resources are well verified and safe enough for Arrow to reach the production quality.

However, Arrow can't do everything. It can't be used to package the whole OS system. Arrow System can be think of part of hostOS or cloud infrastrucre to package and run sigle application. With Arrow System, users do not need to package and ship their own software, instead they only need to ask Arrow System to run some specific applications as Arrows to compose and fullfill their specific goal.     
