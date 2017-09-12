# Lockdown Guide

For production environments, the following procedures are recommended

###Disable Access to Lucee Administrator
If access to the Lucee admin is not necessary to administer the production server, then it is best to disable access via the web server. Below is an example of disabling Lucee admin access in apache. 

>Add to the appache httpd.conf file:

```
#lock down railo web contexts
<Location /lucee>
  Order Deny,Allow
  Deny from all'
</Location>
```

###Move .cfm & .cfc files outside of the webroot
In general, refrain from putting .cfm or .cfc files which are internal to your app in the webroot. Prohibiting internal files from the webroot prohibits unintended access of them. Instead, reference internal files from a component mapping. 

###Disable .CFC dumping
If CFC files cannot be moved out of the webroot, consider disabling the component web dump feature by overwriting {{lucee-web}}/context/conponent-dump.cfm.

###Disable CFC Remoting
If the application does not need use any CFC remoting, disable all calls to CFC by overriding the lifecycle function onCFCRequest(). This sample below will output empty content

```java
function onCFCRequest(string cfcName, string methodName, struct args) {  
	echo('<html><body></body></html>');  
}
```