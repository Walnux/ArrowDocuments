## Arrow Network 

All the Arrow Instances are connected with each other through the standard TCP/IP network. Arrow Service Network module configures and manages the network for each Arrow instance. When Arrow Service Deamon start, it will Setup Linux Bridge if the Bridge is not exist. When shoot an Arrow(start an Arrow Instance), Arrow Service assigns the IP address for individual Arrow Instance, setups the other networking configuation including networkmask, gateway, Macaddress and so on, connects the Arrow Instance on to linux Bridge through Tap device. So by default all the Arrow Instance are connected on the L2 layer of networks. Arrow service also can help to configure the host networks like IPtables and Router to enable portforwarding and NAT and route the network traffic into or outof Arrow System.
For detail of the Arrow Network see diagram below. 

Notes: The current design of Arrow Network is for Arrow 0.1 Prove of Concept Reease. The Arrow Networking compatible with Kubernetes Network and specific VPC of Cloud Network is in plan.  

<p align="center">
  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowNetwork.png">
</p>
