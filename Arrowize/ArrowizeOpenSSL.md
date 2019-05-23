# Arrowize OpenSSL

Most of contents from this page refers [OpenSSL](https://www.openssl.org/docs/OpenSSLStrategicArchitecture.html) OpenSSL is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library. It is used by several key opensource projects for Arrow, like cpython and Node.js.
Let's have a look at it how to Arrowize it.

## OpenSSL architecutre

OpenSSL composed of three parts
* libcrypto. This is the core library for providing implementations of numerous cryptographic primitives. In addition it provides a set of supporting services which are used by libssl and libcrypto, as well as implementations of protocols such as CMS and OCSP.
* libcrypto. This is the core library for providing implementations of numerous cryptographic primitives. In addition it provides a set of supporting services which are used by libssl and libcrypto, as well as implementations of protocols such as CMS and OCSP.
* libssl. This library depends on libcrypto and implements the TLS and DTLS protocols.
* Applications. The applications are a set of command line tools that use the underlying libssl and libcrypto components to provide a set of cryptographic and other features

![OpenSSL architure](/images/OpenSSLArchiture.png)

## OpenSLL Plugin

Typically engines are dynamically loadable modules that are registered with libcrypto and use the available hooks to provide cryptographic algorithm implementations. Usually these are alternative implementations of algorithms already provided by libcrypto (e.g. to enable hardware acceleration of the algorithm), but they may also include algorithms not implemented in default OpenSSL (e.g. the GOST engine implements the GOST algorithm family). Some engines are provided as part of the OpenSSL distribution, and some are provided by external third parties (again, GOST).

* So firtly, to most of usagecases not depending on hardware acceleration or 3rd party algorithms, removing of Plugin support will not have much influence.

* secondly, we need to provided a simple way for user to pickup and builtin the 3rd party algorithms.

## How OpenSLL been used and integrated

* Node.js includes OpenSLL into its own codebase

* cPython _SSL module uses OpenSSL libcrypto, which is depend on the system libcrypto. 
