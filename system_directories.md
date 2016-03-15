# System Directories

On any given platform Lucee installs itself into some standard directories. For framework developers and advanced installations, it can be helpful to know these directories at runtime. Lucee make available some special placeholders that can be expanded within code to these real directories. 

|Directory Placeholder|Description|
| -- | -- |
|{lucee-web}|Path to the lucee web directory, usually {web-root}/WEB-INF/lucee.|
|{lucee-server}|Path to the lucee server directory, usually where the lucee.jar is located.|
|{lucee-config}|This is the same as {lucee-server} in server context and the same as {lucee-web} in web context.|
|{temp-directory}|Path to the temp directory of the current user of the system.|
|{home-directory}|Path to the home directory of the current user of the system.|
|{web-root-directory}|Path to the web root.|
|{system-directory}|Path to the system directory.|
|{web-context-hash}|Hash of the web context.|
|{web-context-label}|A label for the web context. See A note on {web-context-label} below.|

##Using Lucee Directory Placeholders

Use the `expandPath()` method to evaluate a placeholder. The example below shows the results of each placeholder on a Lucee server running on windows via CommandBox. Different operating systems and Lucee installation types will have different results. 

{% gist id="https://gist.github.com/roryl/46ce13d0be02ebf627cb",file="placeholder.cfm" %}{% endgist %}

