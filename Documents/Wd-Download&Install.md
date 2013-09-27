WiperDog is not monolithic software, it need some required software installed.

Before Installing WiperDog solution, check the prerequisite:  
1. Because we are using MongoDB, You need using 64 bit Operating systems.  
2. Java runtime is required to be installed.  
Valid versions are:  

* jre 1.6_30 or greater  
* jre 7  


On the Windows OS, JRE must be 32bit version(this restriction is from the service controlling software we are using).

Download and Install MongoDB
---------------------------------
Visit [mongodb site](http://www.mongodb.org/), then install mongodb to your system(if you dont have it yet)  
We require version 2.2 or above.  

Download and Install XWiki
---------------------------------
Visit [XWiki site](http://www.xwiki.org), then go to "Download&play" -> "XWiki Enterprise".  
Then download XWiki package.  
We recommend you to download "Standalone installer" package.

If you choose "Standalone installer", You just need to unpack zipped package.
After then, XWiki can be started with "startup scripts" placed on the top of unzipped directory.  

Download and Install WiperDog server
---------------------------------
WiperDog server is the control center of WiperDog solution.
You just need to download and unpack to where you like.  
Package(WiperDog server assembly) is located [here](http://develop.wiperdog.org/jenkins/job/wiperdog-assembly-v0.1.0/lastSuccessfulBuild/artifact/target/wiperdog-0.1.0-unix.zip)  
or [here(for Windows)](http://develop.wiperdog.org/jenkins/job/wiperdog-assembly-v0.1.0/lastSuccessfulBuild/artifact/target/wiperdog-0.1.0-win.zip)  
After unpacking the WiperDog assembly, You need to do some 'dirty work'.  
1. You need  to edit bin/wiperdog file

    . /etc/rc.d/init.d/functions  
    
    WIPERDOGHOME=/home/luvina/wiperdog
Change the value of WIPERDOGHOME to the directory you unpacked WiperDog assembly.  
2. You need to edit var/conf/default.params like:

      ],
     dest: [ [ file: "stdout" ] ],
     datadirectory: [
The value of "dest: " is what you need to change, for this version, just change like this:  

    dest: [ [ http: "localhost:13111/spool/tfm_test" ] ],  

Download WiperDog XWiki app then install
---------------------------------
