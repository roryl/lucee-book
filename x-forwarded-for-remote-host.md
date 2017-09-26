# X-Forward-for remote host Header

By default, Lucee \(as of v4.5\) does not configure tomcat for forwarding the user's IP address to Tomcat. This will mean that the CGI.remote\_addr value will display as 127.0.0.1 \(localhost\). To configure this to show the users real IP address, Tomcat needs to be configured to process a header X-Forward-For that Apache sets when proxying the request to Tomcat/Lucee.

## Update Tomcat server.xml

Add the following line just below the opening Engine tag `<Engine name="Catalina" defaultHost="127.0.0.1">`

```xml
<Valve className="org.apache.catalina.valves.RemoteIpValve" remoteIpHeader="X-Forwarded-For" requestAttributesEnabled="true" />
```

When it is all added, it should look like this:

```xml
<Engine name="Catalina" defaultHost="127.0.0.1">
      <Valve className="org.apache.catalina.valves.RemoteIpValve"
               remoteIpHeader="X-Forwarded-For"
               requestAttributesEnabled="true" />
```

Then when dumping the GCI scope, it should now have the remote address instead of 127.0.0.1

## Example Sed Command

If automatically deploying Lucee, the following sed command will find and replace the value into the server.xml file on CentOS

```bash
sed -i -e 's/<Engine name="Catalina" defaultHost="127.0.0.1">/<Engine name="Catalina" defaultHost="127.0.0.1"><Valve className="org.apache.catalina.valves.RemoteIpValve" remoteIpHeader="X-Forwarded-For" requestAttributesEnabled="true" /> /g' /opt/lucee/tomcat/conf/server.xml
```



