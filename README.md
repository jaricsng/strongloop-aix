# strongloop-aix
guide to getting StrongLoop up in AIX 7.1

## Background
The AIX used is provisioned in IBM [PureApplication](http://www.ibm.com/ibm/puresystems/ca/en/pf_pureapplication.html) System W1700-128.

A virtual system pattern (VSP) uses IBM OS Image for AIX Systems  2.1.2.0.

## Overview of tasks
1. Download the required files: IBM NodeJS SDK, libs and make
2. Install the rpms, nodeJS
3. Configure the environment
4. Validate your installation and environment
5. Install StrongLoop
6. Validate StrongLoop

### 1. Download files
For ease of ensuring you can get StrongLoop up and running in AIX, I have placed the following files in ./lib folder in this project.
- IBM nodeJS can be obtained from [here](https://developer.ibm.com/node/sdk/#v4) (Note: I tested with 4.2.2)
- libstdc++-4.8.3-1.aix7.1.ppc.rpm
- libgcc-4.8.3-1.aix7.1.ppc.rpm
- make-3.81-1.aix6.1.ppc.rpm

#### Note:
download object lib from [oss4aix.org](http://www.oss4aix.org/download/RPMS/)
download make from [here](http://www-03.ibm.com/systems/power/software/aix/linux/toolbox/alpha.html)

### 2. Install 
verify you have Java in your AIX envrionment, it is required to install IBM NodeJS SDK

a) install RPMS: 
to intall rpm: 

     > rpm -Uvl libgcc-4.8.3-1.aix7.1.ppc.rpm or rpm -Uvh *.rpm

b) install nodeJS
e.g run 
     
     > ./ibm-4.2.2.0-node-v4.2.2-aix-ppc64.bin
     
details on installation can be found at [NodeJS knowledge centre](http://www-01.ibm.com/support/knowledgecenter/SSWLKB_4.0.0/com.ibm.javascript.4.doc/ia_install.html)

### 3. Configure environment
ensure the following environment variables are set

e.g.

     export PATH=$PATH:/ibm/node/bin
     export LIBPATH=/opt/freeware/lib64
     export LD_LIBRARY_PATH=/opt/freeware/lib/gcc/powerpc-ibm-aix7.1.0.0/4.8.3/ppc64

### 4. Verification
run the following to test node and npm

     > node --version
     > npm --version

expected result for above

     node --version
     v4.2.2
     npm --version
     2.14.7

### 5. Install
(Note: in my envrionment I have disable IPSEC so that I can install from the internet)
#### StrongLoop
run 

     > npm install -g strongloop or npm install --unsafe-perm -g strongloop

#### StrongLoop Process Manager
run 

     > npm install -g strong-pm or npm install --unsafe-perm -g strong-pm

##### Note:
About [StrongLoop](https://strongloop.com/)

To disable ipsec4

     /usr/sbin/rmdev -l ipsec_v4

### 6. Validate strongloop
run 

     > slc loopback

expected result below:

     > slc loopback
          _-----_
         |       |    .--------------------------.
         |--(o)--|    |  Let's create a LoopBack |
        `---------´   |       application!       |
         ( _´U`_ )    '--------------------------'
         /___A___\    
          |  ~  |     
        __'.___.'__   
      ´   `  |° ´ Y ` 
     
     ? What's the name of your application? (loopback) 

### Troubleshooting
checkout 
- https://www.ibm.com/developerworks/community/forums/html/topic?id=ebea5da8-5150-4225-b0f7-147a543ceac4
- http://www.perzl.org/aix/index.php?n=Main.Povray

for any additional aix files missing in your environment you can download it from perzl.org if needed.

# License

This sample code is licensed under [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0).
AIX Toolbox for Linux Applications [license](http://www-03.ibm.com/systems/power/software/aix/linux/toolbox/alpha.html).
