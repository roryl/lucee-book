# Java Virtual Machine

Lucee is a Java servlet application and can be tuned like any Java application. Advanced JVM tuning strategies appropriate for any Java application can also apply to Lucee. This artlce discusses strategies for profiling the JVM and making adjustments. There are two primary tasks for any JVM tuning: monitoring memory and thread usage, and tuning the garbage collection.

For more in depth explanation of the JVM, see these resources:

## Monitoring Memory & Thread Usage

There are two areas to see memory usage by the JVM, in the Lucee administrator, and with the Java Visual VM tool, which is a part of the Java Development kit. The Lucee administrator is good for quick adjustments, and the Visual VM tool is good for complex issues and really understanding what the JVM is doing.

* Lucee getMemoryUsage\(\)
* Visual VM

### Lucee getMemoryUsage

Lucee provides a function 'getMemoryUsage\(\)' which will return the memory in use by the JVM that Lucee is running on. When output, it looks like:

![](memory_usage.png)

### Java Visual VM

#### Configuration

Visual VM is run on a workstation like Windows or OSX, and it connects to a running Lucee server. Visual VM gives a graphical interface to inspect the running JVM process:  
![](/assets/visualvm.png)

To configure Visual VM you will need to install software on your Workstation/Desktop and also the Lucee server

1. [Workstation](#1-workstation)
2. Server
   1. Tomcat Configuration
   2. User Security
   3. Visual VM Script

#### Workstation Configuration

##### 1. Install the JDK

You will need to download/install the Java JDK on your workstation \(not the server!\) to use VisualVM. While backward compatability is sometimes available, as a best practice you should check the version of the JVM you are running tomcat on and use the same JDK verison.

Download URLs change frequently so use this: [https://www.google.com/?\#q=jdk+download](https://www.google.com/?#q=jdk+download)



#### Server Configuration

There are several Tomcat configurations that must be implemented along with a simple script. This article only discusses Tomcat, the default servlet container shipped for a production Lucee installation. At the end of this article there is a sample setup script which will perform all of these tasks.

##### 1. Install the full Java Development Kit

Be sure to install the full Java Development Kit for your installation. The JDK that ships with RedHat based distributions does not have the jstatd binary. For CentOS/RedHat, download the appropriate JDK rpm from Orcale and install it:

```
# Download and install the Java 8 SDK. The oracle site
# requires a specific accept cookie to be set, so we mimic a browser
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u151-b12/e758a0de34e24606bca991d704f6dcbf/jdk-8u151-linux-x64.rpm"
rpm -i jdk-8u151-linux-x64.rpm
```

For CentOS, the JDK will be installed to /usr/java/VERSION/, check the bin folder for the jstatd executable

##### 2.Tomcat Configuration

Update your setenv.sh config to include the following:

> export CATALINA\_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=8999 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=true -Djava.rmi.server.hostname=YOUR.IP.GOES.HERE -Dcom.sun.management.jmxremote.password.file=$CATALINA\_HOME/conf/jmxremote.password -Dcom.sun.management.jmxremote.access.file=$CATALINA\_HOME/conf/jmxremote.access";

Change 'YOUR.IP.GOES.HERE' to the local IP of the server.

You will need to restart tomcat after this change.

##### 3.User Security

You will need to create two files: /opt/lucee/tomcat/conf/jmxremote.access and /opt/lucee/tomcat/conf/jmxremote.password.

jmxremote.access manages permissions and looks like this:

```
userone readwrite
anotheruser readwrite
```

And jmxremote.password is implemented as follows:

```
userone c0mpl3xpass
anotheruser anotherpassword
```

##### 4. Create a Permissions File

Create a JVM permissions file that we will use when starting the visual vm process at /opt/lucee/tomcat/conf/tools.policy with the content:

```
grant codebase "file:\${java.home}/../lib/tools.jar" {
   permission java.security.AllPermission;
};
```

##### 5. VisualVM Script

In order for VisualVM to connect to the running server instance, the jstatd program needs to be running. Its easiest to create a shell script to execute this program:

```
#!/bin/bash
/usr/java/jdk1.8.0_151/bin/jstatd -J-Djava.security.policy=/opt/lucee/tomcat/conf/tools.policy -J-Djava.rmi.server.hostname=YOUR IP ADDRESS GOES HERE
```

Again, update `/your/local/path` as appropriate to the location of the JDK installed in step 1. Save it as `visualvm` or the like, with execute permissions. Run this from the command line while you are running VisualVM and terminate the process when complete.

The following snippet will create the start script

```
##Create a security polity file
cat > /root/bin/visualgc << EOF
#!/bin/bash
#/usr/java/jdk1.6.0_32/bin/jstatd -J-Djava.security.policy=/opt/lucee/tomcat/conf/tools.policy
/usr/java/jdk1.8.0_131/bin/jstatd -J-Djava.security.policy=/opt/lucee/tomcat/conf/tools.policy
EOF
```



