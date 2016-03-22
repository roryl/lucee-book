# Java Virtual Machine

## Enable VisualVM

### Workstation
You will need to download/install the Java JDK on your workstation (not the server!) to use VisualVM. While backward compatability is sometimes available, as a best practice you should check the version of the JVM you are running tomcat on and use the same JDK verison.

Download URLs change frequently so use this: https://www.google.com/?#q=jdk+download

### Server
There are several Tomcat configurations that must be implemented along with a simple script.
#### Tomcat Config
Update your setenv.sh config to include the following:

>export CATALINA_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=8999 -Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=true -Djava.rmi.server.hostname=YOUR.IP.GOES.HERE -Dcom.sun.management.jmxremote.password.file=$CATALINA_HOME/conf/jmxremote.password -Dcom.sun.management.jmxremote.access.file=$CATALINA_HOME/conf/jmxremote.access";

Change 'YOUR.IP.GOES.HERE' to the local IP of the server.

You will need to restart tomcat after this change.
#### User Security
You will need to create two files $CATALINA_HOME/conf/jmxremote.access and $CATALINA_HOME/conf/jmxremote.password. 

jmxremote.access manages permissions and looks like this:
```
userone readwrite
anotheruser readwrite
```
And jmxremote.password as follows:
```
userone c0mpl3xpass
anotheruser anotherpassword
```

#### VisualVM Script
You will want to run jstatd while using Visual VM. There's a bit of parameters so it's easiest to script it:
```
#!/bin/bash
/your/local/path/jdk/jre/bin/jstatd -J-Djava.security.policy=/your/local/path/tomcat/conf/tools.policy
```
Save it as `visualvm` or the like, with execute permissions. Run this from the command line while you are running VisualVM and terminate the process when complete.