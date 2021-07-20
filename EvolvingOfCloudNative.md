# The Evolving of Cloud Native

## Summary 
Figuring out Cloud Native evolving direction can help us find and prepare for the potential opportunities in the fast growing cloud native technology and community which is important for our businesses. The Cloud Native evolving is the process to isolate the common distributed cloud application requirements and challenges and work on the innovations to fulfill these requirements and resolve the challenges. 
These requirements and challenges can be summarized from the 12-Factor App[8] principles and the challenges to develop and operate the Microservices[9] or Monolith applications with Poly-cloud or Single-cloud strategies. They can be divided into 4 categories – Lifecycle, Networking, Binding and State[2]. 
 
## Distributed Cloud Application Requirements 
Obviously, Business Logic is the centric of a distributed cloud application which is used to implement some specific features for the customers. However, serving users with these features through Internet as a cloud service is a huge challenge for every people from individual cloud application developers to entrepreneurs and enterprises who run their businesses on Internet and cloud. Because a lot of Business Logic irrelevant requirements have to be fulfilled through the entire lifecycle of a cloud application. 
- From the early monolithic architecture cloud application stage, the distributed cloud application design principles were summarized in 12-Factor App, which is still be taken as the Bible for developing the distributed cloud application. 
 
- In the past 2 decades,  most internet companies have been experiencing the fast organization expanding, which brings the cooperation, management and organization culture shifting challenges. The monolithic environment leads to bigger stakeholder meetings, and more complicated decision making process because of the interwoven logic and shared data that impact the performance of all the teams[5]. Making use of microservices architecture is the best way for industrial to resolve the challenge. 
 
- Recently, more and more users tend to deploy their microservices on multiple Public Cloud and use the cloud services from different Public Cloud providers. The adoption of the hybrid clouds like Private cloud, Edge cloud and public cloud simultaneously is the new requirement for distributed cloud application. The combination of hybrid cloud and multi-cloud is called poly-cloud. For poly-cloud, the microservices communication among different clouds  infrastructure behind individual network firewall and configuration becomes the challenge. The other challenge comes from the infrastructure management of the different clouds infrastructures. There are two kind of solutions addressing the challenge. Thery are the multi-clusters solution and Cloud centric clusters. They are both based on Kubernetes and Container technology. OpenYurt on which we are working with Alibaba is the Cloud centric non-invasive Kubernetes solution. 
 
What needs to be emphasized is that Microservices and Monolith will coexists as the two application architecture options. The using of specific architecture mainly decided by the complexity of the organization who develops and operates the application. At same time Single-cloud and poly-cloud strategies should also coexists and be adopted by different types of users basing on their business requirments.   
 
Consequently, the Distributed Cloud Application Requirements can be summarized from the 12-Factor App principles and the challenges to develop and operate the Microservices or Monolith applications with Poly-cloud or single-cloud strategies. 
 
The business logic irrelevant distributed cloud application requirements which are divided into 4 categories can be demonstrated in blow diagram.
<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/CloudNativeRequiremnts.png">
</p>

-	Lifecycle - it is in charge of the entire lifecycle of the distributed cloud application from developing, packaging, releasing  deploying to scaling upgrading etc. Kubernetes as well as Container technology not only decouples these fundamental features from the Business Logic but also provides the extensible framework for users to add new Distributed Cloud Application Features with the standard Control and Operator Design Patten. Wide adoption of Kubernetes as the cloud infrastructure bring cloud industrial into Cloud Native era. 
 
-	Networking - Once the Monolithic Applications are divided into many independently evolving and interconnecting Microservices. Networking – the second category of requirements becomes the real pain point for the Cloud Native Applications. Service Mesh technology emerged recently to resolve the complexity of interconnecting of the microservices targets for the pain point. "Envoy" based Istio project and Linkerd project are the two main popular service mesh solutions. To resolve the connection challenge among the Microservices deployed on different cloud infrastructure hosted behind different (L3-L4)Network configuration. Skupper[27] project based on AMQP[28] protocol implements the layer 7 network for native Kubernetes worth our attention. Virtual Application Network(VAN)[28] and the Service Mesh technology might be the good solution for resolving the Networking challenges for Cloud Native. 
 
-	Binding - Distributed Cloud Application must depend on the services either from the Cloud service Providers or local or Edge services. Normally these services are called Backend as a Service (BaaS). To access the specific BaaS, the specific BaaS SDK has to be involved into the application development. So the applications have to be closely bound with the BaaS as well as the specific Cloud environment. To use Poly-Cloud, users don't want their applications attaching to a specific BaaS and Cloud provider. So the standard API for the application to call the BaaS is a key requirements. Dapr[4] project is designed for this goal. 
 
-	State - Handling the states among the scaled Microservices as well as the multiple instances of the same microservice across the different cloud environments is another common challenges for most of distributed cloud applications. The proper handling of Application state influences the performances and complexity of Distributed Cloud Applications. Dapr and Cloudstate[23] project are the pioneer projects addressing the state requirements.     
 
## The Cloud Native trend 
Combining the understanding of Cloud Native Envolving with our past several years' experience working closely with the top players in Cloud Native, the prediction of three Cloud Native trends is summarized. 
 
-	Decoupling – The distributed cloud application common features (requirements implementations) are decoupling from the business logic. As mentioned above, Kubernetes not only decouples the lifecycle features from the development of the cloud application but also provides the extensible framework for implementation of the other features. Nowadays, the Distributed Run-time Microservices architecture is more and more used by many cutting edge innovations. The runtimes providing the common features are deployed as the sidecars of the microservices which focus on the specific business domain logic. Dapr (Distribute Application Runtime) project, Scupper project, Cloudstate project and Service Mesh technologies are all based on this Distributed Run-time Microservices Architecture. With this architecture, the application developers can focus on their business logics, which is the final goal of decoupling trend. However, Distributed Run-time Microservices Architecture increases the system complexity and latency. The Operator and Application API Standardizing and Distributed Cloud features sinking are the another two trends to resolve these issues.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/decoupling.png">
</p>

- Standardizing – The Operator and Management features as well as the declarative APIs provided by many different cloud native projects might overlap and even conflict. Selecting and configuring these features and APIs is complicated and easy to be broken. Cloud Native community try to resolve the problem by setting up the standard high level APIs for operators to manage the applications without touching the low level API details. KubeVela[21] project sponsored by Alibaba focuses on the Open Application Mode and targets to provide users the standard way to run an Cloud Native application. Knative - the popular project for serverless workload sponsored by Google also defined the standard high level APIs for the Serverless and Faas workload. Although Service Mesh technology is still not been widely adopted, the trend to standardizing the Networking API is also quite clear. And the Layer 7 Network technology like Virtual Application Network(VAN) supported by RedHat might also become one of the standard for Cloud Native network solutions for connecting poly-cloud. Above Operator and Management features and APIs are transparent to Application developers. The application developer aware API now becomes more and more important. In order not to be bound with a specific cloud environment and facilitate the common state handling, Cloud Native community start to work on defining the standard Cloud Native Application API. Dapr project and the Cloudstate project are the good examples. Knative also provides the Event message API basing on cloud event specification hosted by CNCF. The cloud native API standardizing can be demonstrated in blow diagram. Although API standardizing can resolve the complexity issue in some degree, the best way to resolve the complexity and latency issue is distributed cloud feature sinking.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/standardizing.png">
</p>

-	Sinking – The common distributed cloud features are sinking from Application to platform. At same time, with the API standardizing and the feature implementation stabilizing, some of the performance critical features are sinking to the Hardware layer. It is another very important trend for us. In past years, we worked on several this kind of features. Alibaba Xdragon platform implements the network and storage virtualization features in the hardware layer through FPGA technology. AWS has the similar hardware platform called Nitro[25]. As the general version of Alibaba Xdragon and AWS Nitro hardware platform, SmartNIC solution becomes more and more popular and adopted by many mainstream Public Cloud Providers like Microsoft Azure[24]. Another good sinking example is Intel HWDRC technology. Working on the sinkable features from Cloud Native platform to Hardware layer might help us workout the new features to differentiate our hardware platform.

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/sinking.png">
</p>

## Conclusion 
Cloud Native technologies and community are evolving very quick to resolve the challenges from the traditional monolith application to Microservices and the latest poly-cloud requirements. Although cloud native technology is changing very quickly, we still can figure out its important trends - Decoupling, API Standardizing and Feature Sinking. The pioneer projects like Dapr, Cloudstate, Skupper, KubeVela and OpenYurt who are leading the evolving process are worth our attention. The most important trend is the platform features sinking to Hardware platform. It is the final solution to resolve the complexity and latency issue of Cloud Native. 

## References: 
- [1] [How Alibaba use Dapr](https://blog.dapr.io/posts/2021/03/19/how-alibaba-is-using-dapr/) 
-	[2] [Multi-Runtime Microservices Architecture by Bilgin Ibryam](https://www.infoq.com/articles/multi-runtime-microservice-architecture/) 
-	[3] [Dapr github](https://github.com/dapr/dapr) 
-	[4] [Dapr Documents](https://docs.dapr.io/concepts/)
-	[5] [Github: from monolith to microserivces](https://www.infoq.com/presentations/github-rails-monolith-microservices/?itm_campaign=rightbar_v2&itm_source=infoq&itm_medium=presentations_link&itm_content=link_text)
-	[6] [Airbnb: from monolith to microservice](https://www.youtube.com/watch?v=NxDjKKj4bQE)
-	[7] [When To Use Microservices (And When Not To!)](https://www.youtube.com/watch?v=GBTdnfD6s5Q)
-	[8] [12 factor App](https://12factor.net/)
-	[9] [Martin Fowler' Microservice website](https://martinfowler.com/microservices/)
-	[10] [distributed caching](https://dzone.com/articles/where-is-my-cache-architectural-patterns-for-cachi)
-	[11] [The Evolution of Distributed Systems on Kubernetes](https://www.infoq.com/presentations/kubernetes-primitives-design-patterns/?utm_source=presentations&utm_medium=london&utm_campaign=qcon)
-	[12] [Workflow engine](https://workflowengine.io/blog/java-workflow-engines-comparison/)
-	[13] [Workflow & Dapr](https://workflowengine.io/blog/java-workflow-engines-comparison/)
-	[14] [ideompotency](https://www.restapitutorial.com/lessons/idempotency.html#:~:text=From%20a%20RESTful%20service%20standpoint,as%20making%20a%20single%20request.)
-	[15] [RESTful API](https://www.restapitutorial.com/lessons/whatisrest.html)
-	[16] [Saga distributed transaction](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga#:~:text=A%20saga%20is%20a%20sequence,that%20counteract%20the%20preceding%20transactions.)
-	[17] [Deployment strategy](https://searchitoperations.techtarget.com/answer/When-to-use-canary-vs-blue-green-vs-rolling-deployment#:~:text=Blue%2Fgreen%2C%20which%20requires%20a,option%20due%20to%20infrastructure%20limitations.)
-	[18] [Why Linkerd doesn't use Envoy](https://linkerd.io/2020/12/03/why-linkerd-doesnt-use-envoy/#_ga=2.184394479.830314843.1621890250-1976985841.1621890250)
-	[19] [istio Traffic Management](https://istio.io/latest/docs/concepts/traffic-management/)
-	[20] [Knative sample](https://knative.dev/docs/serving/samples/)
-	[21] [KubeVela](https://kubevela.io/docs/concepts/#environment)
-	[22] [Knative eventing](https://knative.dev/docs/eventing/)
-	[23] [CloudState](https://cloudstate.io/docs/working.html)
-	[24] [Do Smart Network Cards Have a Future Outside the Hyperscale Data Center?](https://www.datacenterknowledge.com/networks/do-smart-network-cards-have-future-outside-hyperscale-data-center)
-	[25] [aws-nitro-system](https://perspectives.mvdirona.com/2019/02/aws-nitro-system/)
-	[26] [AMQP](https://www.youtube.com/watch?v=g3e9lDlMn5M&t=2457s)
-	[27] [skupper](https://skupper.io/community/index.html)
-	[28] [VAN & skupper architecture](https://developers.redhat.com/blog/2020/01/01/skupper-io-let-your-services-communicate-across-kubernetes-clusters)
