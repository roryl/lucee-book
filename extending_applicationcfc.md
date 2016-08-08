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


