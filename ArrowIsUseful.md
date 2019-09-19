# Moden cloud needs a simple, secure, low latency and overhead way to run software

## What are the trends of moden cloud?
Cloud era brought revolution of computerization world. This revolution created a huge and fast growing market<sup>[1](https://www.statista.com/statistics/510350/worldwide-public-cloud-computing/)</sup>.

Traditional [Cloud Infrastuctre as a Service (IaaS)](https://en.wikipedia.org/wiki/Infrastructure_as_a_service) liberates individuals and orgnizations from the burden to maintain their physical servers and infrastrucre on premise. People just rent the scalable virtual servers as well as other resources from the Cloud Service Providors(CSP) like [AWS](https://aws.amazon.com/). The central manangement of cloud infrastrucrue greatly promots the efficency to use the computing, netwroking and storage resources. 

Cloud technologies and market are developing very quickly. what are the trends of moden cloud?
- [Serverless computing](https://en.wikipedia.org/wiki/Serverless_computing)

Serverless Computing will liberate cloud users from maintaining the complicated servers and cloud infrastructure. People can focus on their applicatons and just run these applications on the could.

The global serverless architecture market size is expected to reach USD 19.84 billionby 2025 at a 26.0% CAGR during the forecast period, according to a new study by Grand View Research, Inc.<sup>[4]</sup>

- CSP Edge Computing

CSP Edge Computing extends computing resources from cloud to users' premise where the data are created. It closely binds Internet of Things (IoT) with Cloud, and will greatly promote the booming of IoT and Cloud market.

The global edge computing market size is expected to reach USD 28.84 billion by 2025 registering a CAGR of 54.0%, according to a new report by Grand View Research, Inc.[?](https://www.grandviewresearch.com/press-release/global-edge-computing-market)

Serverless computing technoloies are widely used by CSP Edge Computing on moden Cloud. The applications and serverless framework software have to flow and run from Cloud infrastructure to Edge computering resources. The good example is [AWS Lambda]() 
 
Security is the top priority to Cloud computing. User applications even framework software should be run in secure environemnt both on edge and cloud. Serverness computering requires the software be started instantly with very low latency to response the event or handle data from IoT devices. Becuase of the limitted resources on IoT and Edge computing the software should be run with low overhead.  

- Optimization on traditional LAMP stack

## Industrial is waiting for a safe simple agile and low overhead workload to push cloud forward

Currently, the main workload in cloud is traditional full feature Virtual Machine with the full feature guest OS, middlewares and libraris to run applications. It is very redundant and slow. And the overall infrastrucure is also quite complicated. 

Recent years, Container like Docker comes to dominate the cloud workload. Containers can be used to package, ship and run the software isolated directly on the hostOS. Containers share the same kernel which greatly increases the code running indensity and efficiency. But container is not sandbox. Security and stability is a problem. Besides Container like docker container implementaion is very complicated . And not easy to be used at some resource limtted edge computing environemnt or some FaaS solution directly like AWS Greengrass. Furthermore, although Docker Container can be used to package single application, most people still tend to use it to package the whole system ever running on the virtual Machine. That is one of the reason why docker container suceed. But it can't help the whole cloud and edge ecosystem small and simple.

Arrow shares some basic views with Unikernel like run single application on Virutal Machine. But Arrow is actually differnt solution with Unikernel. Unikernel is the libOS which link application with the specific OS libearis and run on VM. While Arrow makes use of existing mature Linux Kernel. And Application runs on the standarnd Linux environment. So Arrow can make full use of exising Linux resources. Most importantly most of these resources are well verified and safe enough for Arrow to reach the production quality.

However, Arrow can't do everything. It can't be used to package the whole OS system. Arrow System can be think of part of hostOS or cloud infrastrucre to package and run sigle application. With Arrow System, users do not need to package and ship their own software, instead they only need to ask Arrow System to run some specific applications as Arrows to compose and fullfill their specific goal.     

[1] [Total size of the public cloud computing market from 2008 to 2020](https://www.statista.com/statistics/510350/worldwide-public-cloud-computing/)
[2] [Infrastrutur as a Service (IaaS)](https://en.wikipedia.org/wiki/Infrastructure_as_a_service)
[4] https://www.grandviewresearch.com/press-release/global-serverless-architecture-market
