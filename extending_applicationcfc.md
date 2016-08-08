# Extending Application.cfc

Because the Application.cfc is a regular component, it can extend any component to implement functionality. This is useful for building reusable frameworks or overriding behavior in subdirectories of a web application.

To have an Application extend another, use the extends attribute on the Application.cfc. Consider these files in a webroot:

* /
  * baseApp.cfc
  * Application.cfc
  * index.cfm

Wherein this example, baseApp.cfc implements the functionality, and Application.cfc extends it:

{% gist id="roryl/3ea2df6b346a2425875e630e4b6f5fe6",file="baseApp.cfc" %}{% endgist %}

{% gist id="roryl/3ea2df6b346a2425875e630e4b6f5fe6",file="Application.cfc" %}{% endgist %}

If this application is run, it will output the text from the baseApp.cfc because it was the Application.cfc that extended it, and Applictation.cfc is run on every request: 

> This is my base component that applications can extend

##Extending Application.cfc in parent folders

Sometimes it is necessary to extend another Application.cfc in a parent or root folder. Component extensions are pathed from the current directory, from the webroot, or from a mapping. For any other component (not named Application.cfc) this is not an issue. But when an Application.cfc is extending another Application.cfc, it can cause a stackoverflow error (because it thinks it is extending itself), since Lucee looks in the current direcotry for the component name. 

Consider this directory structure: 

* /
  * Application.cfc
  * subfolder1/
    * Application.cfc
    * index.cfm

If the Sub application wants to extend the root Application, it needs to prepend the extends attribute with a period. This tells Lucee to look at the webroot, and not the current directory, for the component.

/subfolder1/Application.cfc
```
component extends=".Application" {

	writeOutput("Output from /subfolder1/Application.cfc <br />");

}
```

/Application.cfc
```
component {

	writeOutput("Output from /Application.cfc <br />");

}
```

if the /subfolder1/Application.cfc nievely had `component extends="Application"` without the period, then Lucee will try to have the Application.cfc extend itself, and this will lead to an irrecoverable error.

When running this web application and going to /subfolder1/index.cfm, it will output the following:

```
Output from /Application.cfc 
Output from /subfolder1/Application.cfc 
```

