## Python overview 

Python is an interpreted, high-level and general-purpose programming language. Given its accessible and versatile nature, it is among the top popular languages in the world. So, Python is one of the main program Languages Arrow should support. 

 

## Python and Arrow 

In current Arrow 0.1 release, the basic support for Arrow has been added. Python Application can run on Arrow as Below steps 

## Run Python Applications on Arrow 

After [ASDK] and [Arrow Service] is installed. Python Arrow Binary, [Python Arrow Meta](https://github.com/Walnux/ameta/tree/master/python) and Python sample application [python-web](https://github.com/Walnux/ameta/tree/master/python-web) has been preinstalled in the developing machine. 

- Run below command in Arrow Service source directory 

``` shell 

$ sudo ./bin/actrl shoot python 

$ sudo ./bin/actrl logs 

... 

 Python 3.8.0a4 

``` 

Python Arrow Meta is located at: /path/to/arrowd/.work/var/arrowd/pieces/meta/python  

Have a look at file arrow_spec.json in the directory 

``` json 

{ 

    "binary": { 

        "name": "python", 

        "version": "v3.8", 

        "project": "https://github.com/python/cpython" 

    }, 

  

    "process": { 

        "terminal": false, 

        "cmd": "python", 

        "args": [ 

            "python", 

            "--version" 

        ] 

    } 

} 

``` 

Python 3.8 is used and command: "python –version" is run when shooting Arrow python  

- run python-web application 

``` shell 

$ sudo ./bin/actrl shoot python-web 

$ sudo ./bin/actrl logs 

... 

serving at port 8080 

... 

``` 

Have look at file arrow_spec.json 

``` json 

{ 

    "binary": { 

        "name": "python", 

        "version": "v3.8", 

        "project": "https://github.com/python/cpython" 

    }, 

  

    "process": { 

        "terminal": false, 

        "cmd": "python", 

        "args": [ 

            "python", 

            "server.py" 

        ] 

    }, 

  

    "port": 8080, 

    "export": 3008, 

    "proto": "tcp" 

} 

``` 

Python-3.8 Arrow Binary is used; When shooting python-web, command: python server.py is run; the web server is serving in port 8080, and the service is exported through port 3008. 

The web server can be accessed through http://localhost:3008. 

``` shell 

martin@nuc8:~/go/src/github.com/Walnux/arrowd$ wget http://localhost:3008 

--2020-10-06 20:14:43--  http://localhost:3008/ 

Resolving localhost (localhost)... 127.0.0.1 

Connecting to localhost (localhost)|127.0.0.1|:3008... connected. 

HTTP request sent, awaiting response... 200 OK 

Length: 247 [text/html] 

Saving to: ‘index.html.22’ 

  

index.html.22                                      100%[================================================================================================================>]     247  --.-KB/s    in 0.002s   

  

2020-10-06 20:14:43 (155 KB/s) - ‘index.html.22’ saved [247/247] 

 

``` 

Using web browser to access the web server. 

<p align="center"> 

  <img src="https://github.com/Walnux/ArrowDocuments/blob/master/images/python-web.jpg"> 

</p> 

Have a look at the server.py application 

``` python  

import http.server 

import socketserver 

  

PORT = 8080 

Handler = http.server.SimpleHTTPRequestHandler 

  

with socketserver.TCPServer(("", PORT), Handler) as httpd: 

    print("serving at port", PORT) 

    httpd.serve_forever() 

``` 

http.server and socketserver module in Python Standard Library is imported to implement this simple webserver. 

Notes: in the future, the Python Standard Library will be moved to Python Arrow Binary from Python Arrow Meta, so user application doesn’t have to package with Python Standard Library. 

User can use Python Arrow Meta and Python-web Arrow Image as example to develop his/her own application. 

- Run user python-hello Application on Arrow 

``` shell 

martin@nuc8:~/go/src/github.com/Walnux/arrowd$ sudo make asdk 

#Enter ASDK 

docker start -i adasdk 

/ #cd admeta 

/admeta # cp python python-hello -r 

``` 

## Supporting Python on Arrow
### Staticly link Python Runtime
[See CPython Building Process](https://github.com/python/cpython/blob/master/Modules/Setup)

also Reference: [Staticly Link Python](https://stackoverflow.com/questions/1150373/compile-the-python-interpreter-statically)

* using GNU Libc to staticly link Python lead to below warnings
```Console
/home/martin/repo/cpython/./Python/dynload_shlib.c:98: warning: Using 'dlopen' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
libpython3.8m.a(posixmodule.o): In function `posix_getgrouplist':
/home/martin/repo/cpython/./Modules/posixmodule.c:6678: warning: Using 'getgrouplist' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
libpython3.8m.a(grpmodule.o): In function `grp_getgrall_impl':
/home/martin/repo/cpython/./Modules/grpmodule.c:280: warning: Using 'getgrent' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
libpython3.8m.a(grpmodule.o): In function `grp_getgrgid_impl':
/home/martin/repo/cpython/./Modules/socketmodule.c:6402: warning: Using 'getaddrinfo' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
libpython3.8m.a(spwdmodule.o): In function `spwd_getspall_impl':
/home/martin/repo/cpython/./Modules/spwdmodule.c:174: warning: Using 'getspent' in statically linked applications requires at runtime the shared libraries from the glibc version used for linking
```

Investigation:

 * 1. dlopen(): glibc use dlopen() and related functions to dynamically insert plugin at runtime. Since Plugin insertion needs involving all the dynamically linking process and the whole glibc library. So when you static linking something, GCC with glibc will show the warning message. for detail of Dlopen please See [Why Musl dose not support dlopen() on static linking] ()
I believe what Musl has done is reasonable. Arrow will not support plugin since Plugin brings security and
stability issues and costs extra maintaining efforts.
 * 2. getaddrinfo(): this function needs toch DNS, glibc may insert Libnss to implement several differnt DNS solutions. That involves dlopen() as metioned above. I do not think it is the right thing for glibc the so foundamental libary to call other libraries. [Musl has better solution here]() to implement the public protocol to support all the DNS solutions. 
 * 3. after check Glibc code on getgrouplist(). It also will use libNSS, so report the similar warning. 
 ``` code c
glibc/nss/nsswitch.h
/* Warning for NSS functions, which don't require dlopen if glibc
   was built with --enable-static-nss.  */
#ifdef DO_STATIC_NSS
# define nss_interface_function(name)
#else
# define nss_interface_function(name) static_link_warning (name)
#endif
 ```
 
 ``` console
martin@walnut:~/repo/glibc$ grep "static_link_warning" * -r
dlfcn/dlmopen.c:static_link_warning (dlmopen)
dlfcn/dlopen.c:static_link_warning (dlopen)
include/libc-symbols.h:#define static_link_warning(name)
include/libc-symbols.h:#define static_link_warning(name) static_link_warning1(name)
include/libc-symbols.h:#define static_link_warning1(name) \
nss/nsswitch.h:# define nss_interface_function(name) static_link_warning (name)
 ```
 Obviously, only dynamical linking dlmopen/dlopen and depend on Libnss will cause the warning. And we have two options to resolve the problem. 
* First is to use staticly linked glibc and
* the second is to use Musl

We prefer to start from the latter

### Packaging & Distribution for Python Application on Arrow 
The current Arrow 0.1 release only supports the basic Python Standard Library based application for Prove of Concept. 

It is very important to explore a proper way to package python applications for the Single Task Arrow System which is compatible with existing Python packaging and distribution mechanisms. 

[see An Overview of Packaging for Python ](https://packaging.python.org/overview/#thinking-about-deployment)
[see Python Binary Extention ](https://packaging.python.org/guides/packaging-binary-extensions/)

User can make use of ASDK to staticly link their needed Binary Extension Modules into Python runtime.

The inital idea is:
directly link binary extension with "libpythonxy.a" which is ar from all the python modules and Programs/python.o. see below compile message. This does not need to rebuild all the cyphon. And it should be very quick. 
```
ar rcs libpython3.8m.a Modules/getbuildinfo.o Parser/acceler.o Parser/grammar1.o Parser/listnode.o Parser/node.o Parser/parser.o Parser/token.o  Parser/myreadl    ine.o Parser/parsetok.o Parser/tokenizer.o Objects/abstract.o Objects/accu.o Objects/boolobject.o Objects/bytes_methods.o Objects/bytearrayobject.o Objects/byt    esobject.o Objects/call.o Objects/cellobject.o Objects/classobject.o Objects/codeobject.o Objects/complexobject.o Objects/descrobject.o Objects/enumobject.o Ob    jects/exceptions.o Objects/genobject.o Objects/fileobject.o Objects/floatobject.o Objects/frameobject.o Objects/funcobject.o Objects/interpreteridobject.o Obje    cts/iterobject.o Objects/listobject.o Objects/longobject.o Objects/dictobject.o Objects/odictobject.o Objects/memoryobject.o Objects/methodobject.o Objects/mod    uleobject.o Objects/namespaceobject.o Objects/object.o Objects/obmalloc.o Objects/capsule.o Objects/rangeobject.o Objects/setobject.o Objects/sliceobject.o Obj    ects/structseq.o Objects/tupleobject.o Objects/typeobject.o Objects/unicodeobject.o Objects/unicodectype.o Objects/weakrefobject.o Python/_warnings.o Python/Py    thon-ast.o Python/asdl.o Python/ast.o Python/ast_opt.o Python/ast_unparse.o Python/bltinmodule.o Python/ceval.o Python/codecs.o Python/compile.o Python/corecon    fig.o Python/dynamic_annotations.o Python/errors.o Python/frozenmain.o Python/future.o Python/getargs.o Python/getcompiler.o Python/getcopyright.o Python/getpl    atform.o Python/getversion.o Python/graminit.o Python/import.o Python/importdl.o Python/marshal.o Python/modsupport.o Python/mysnprintf.o Python/mystrtoul.o Py    thon/pathconfig.o Python/peephole.o Python/preconfig.o Python/pyarena.o Python/pyctype.o Python/pyfpe.o Python/pyhash.o Python/pylifecycle.o Python/pymath.o Py    thon/pystate.o Python/context.o Python/hamt.o Python/pythonrun.o Python/pytime.o Python/bootstrap_hash.o Python/structmember.o Python/symtable.o Python/sysmodu    le.o Python/thread.o Python/traceback.o Python/getopt.o Python/pystrcmp.o Python/pystrtod.o Python/pystrhex.o Python/dtoa.o Python/formatter_unicode.o Python/f    ileutils.o Python/dynload_shlib.o    Modules/config.o Modules/getpath.o Modules/main.o Modules/gcmodule.o Modules/posixmodule.o  Modules/errnomodule.o  Modules    /pwdmodule.o  Modules/_sre.o  Modules/_codecsmodule.o  Modules/_weakref.o  Modules/_functoolsmodule.o  Modules/_operator.o  Modules/_collectionsmodule.o  Modul    es/_abc.o  Modules/itertoolsmodule.o  Modules/atexitmodule.o  Modules/signalmodule.o  Modules/_stat.o  Modules/timemodule.o  Modules/_threadmodule.o  Modules/_    localemodule.o  Modules/_iomodule.o Modules/iobase.o Modules/fileio.o Modules/bytesio.o Modules/bufferedio.o Modules/textio.o Modules/stringio.o  Modules/fault    handler.o  Modules/_tracemalloc.o Modules/hashtable.o  Modules/symtablemodule.o  Modules/arraymodule.o  Modules/cmathmodule.o Modules/_math.o  Modules/mathmodu    le.o Modules/_math.o  Modules/_contextvarsmodule.o  Modules/_struct.o  Modules/_weakref.o  Modules/_testcapimodule.o  Modules/_randommodule.o  Modules/_element    tree.o  Modules/_pickle.o  Modules/_datetimemodule.o  Modules/_bisectmodule.o  Modules/_heapqmodule.o  Modules/_asynciomodule.o  Modules/_json.o  Modules/unico    dedata.o  Modules/fcntlmodule.o  Modules/spwdmodule.o  Modules/grpmodule.o  Modules/selectmodule.o  Modules/mmapmodule.o  Modules/_csv.o  Modules/socketmodule.    o  Modules/_cryptmodule.o  Modules/nismodule.o  Modules/termios.o  Modules/resource.o  Modules/md5module.o  Modules/sha1module.o  Modules/sha256module.o  Modul    es/sha512module.o  Modules/sha3module.o  Modules/blake2module.o Modules/blake2b_impl.o Modules/blake2s_impl.o  Modules/syslogmodule.o  Modules/binascii.o  Modu    les/parsermodule.o  Modules/zlibmodule.o  Modules/multibytecodec.o  Modules/_codecs_cn.o  Modules/_codecs_hk.o  Modules/_codecs_iso2022.o  Modules/_codecs_jp.o      Modules/_codecs_kr.o  Modules/_codecs_tw.o Python/frozen.o

gcc -pthread -static -static    -o python Programs/python.o libpython3.8m.a -lcrypt -lpthread -ldl  -lutil -lm -lnsl             -L/usr/local/lib -lz         -    lm 
```
