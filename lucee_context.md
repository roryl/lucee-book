# Lucee Context

Lucee can be installed on a server and serve many different domain names simultaneously. When running Lucee, each domain name gets its own distinct "Context" which securely separates the Lucee process from one domain to another.  There is one *Server Context* for a Lucee installation that all domains share , and one *Web Context* for each domain name. These Context's are created the first time a domain is loaded.

##Server Context
The Server Context is the Lucee process which is global to all Web Context's (domain names). The Server Context is used so that all Web Contexts utilize the same configuration when necessary. This is common when the same configuration should apply to every domain name on the server.

##Web Context
Each domain being served by Lucee will automatically get its own Web Context. This allows specific settings to be set for a domain which are separate from the Server Context.

The settings for the Web Context are created in the webroot of the running website, in a folder called WEB-INF. If WEB-INF is deleted, all Web Context settings will be deleted and it will be recreated on the next time Lucee runs. 