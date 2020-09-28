## Arrow System Working Mode 

In theory, to run an application, only two essential parts are required, application binary and the configuration about how to run the application. If the same (release/version of) application is run at the same physical node by different users or the same user with different configurations. The only difference is the configuration, the application binary should be shared and doesn’t have to be packaged into individual package. So, on the same physical node, normally, only one copy of the application binary needs to be download and saved. Because the application binary is statically linked, the binary size is very small, some popular applications binaries like Nodejs, python runtime even can be preinstalled as part of Host Operating System. This can greatly decrease the application loading latency, and save the network bandwidth and system resources. 

Before introducing Arrow System Working Mode, several key concepts have to explained. 

**ISV (Independent Software Vendor)**: provides the software that may be used by the users to build his/her microservice. NGINX, Python runtime, Nodejs runtime, Redis and many other popular software are provided by ISV. Nowadays, most software provided by ISV are open sourced and developed in open source community. 

**Users**: The developers who use the software provided by ISVs to develop his/her own microservices 

**Arrow Binary**: The statically linked application binary, normally it is the ELF style.  

**Arrow Meta**: The template files provided by ISV who provides the Arrow Binary and instructs Users how to run the application(software). Normally template Arrow configuration Spec file, application configuration files, Confidential, static Data, Application scripts and so on are included into Arrow Meta  

**Arrow Market**: is Composed of the repositories of ISVs and Users to save the Arrow Binary, Arrow Meta and Arrow Meta. 

**Arrow Image**: Users downloads the Arrow Meta and populate the user specific configuration data and files to build the Arrow Image. This Image can be uploaded to Arrow Market and then run on the specific Cloud, Edge computing environment. 

Notes: Arrow Image doesn’t include any complied Application binary, it only specifies what Arrow binary will be run, and how to run it. The other important part is the application scripts for interpreted languages.   

**ASDK (Arrow System Development Kit)** helps users to develop, debug, create and upload Arrow Binary, Arrow Meta or Arrow Image.  

See the Arrow System working mode below: 

<p align="center"> 

  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowWokingMode.png"> 

</p> 


## Example 

## Example 

Diagram below demonstrates a typical usage case of Arrow System Working Mode. 

The same user uses the same release of Nodejs to develop and run different Nodejs services. The first application is Hello world! The second is the chatting room application. 

If Arrow System on your Machine has been set up, [run Nodejs applications as Arrow Instance]() can be used to try this usage case which can help to understand Arrow System Working Mode. 

Notes: Arrow Market is still in plan. This example uses local Arrow System environment to verify the concept.       

 <p align="center"> 

  <img src="https://github.com/Walnux/Arrow_Documents/blob/master/images/ArrowWokingModeExample.png"> 

</p> 
