# Server Scope
Lucee makes available a Server scope which contains a lot of useful information about the running Lucee server. The specific details returned depend on the operating system running Lucee. These examples below are run on Windows.

##Dumping the server scope
To quickly see what is in the server scope, use `writeDump()`:

{% gist id="roryl/a8fa01f1423014d8ce5faceb063d33b3",file="server_scope.cfm" %}{% endgist %}

It will return a structure.



