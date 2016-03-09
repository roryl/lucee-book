# Lucee Context

Lucee can be installed on a server and serve many different domain names simultaneously. When running Lucee, each domain name gets its own distinct "Context" which securely separates the Lucee process from one domain to another.  There is one *Server Context* for the entire server, and one *Web Context* for each domain name. These Context's are created for you the first time your website runs on a server.

##Server Context
The Server Context is the Lucee process which is global to all Web Context's (domain names). The Server Context can be configured so that all Web Contexts utilize the same configuration. This is common when the same configuration should apply to every domain name on the server

##Web Context
Each domain being served by Lucee will automatically get its own Web Context so that specific settings can be maintained for this domain name which are separate from the Server Context.

The settings for the Web Context are created in your webroot in a WEB-INF folder. If you delete this folder, all settings will be deleted and it will be recreated on the next time Lucee runs. 