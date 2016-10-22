# Applications
Lucee has a concept of "Applications" (as in Web Applications) which provide a context for the code which is running. All code runs within an Application context, and the Lucee runtime provides hooks and settings for controlling the lifecycle of a web application (starting, stopping, requests, responses) and configuration (class paths, databases, clustering, mail settings, and much more)

By default, the Application that code will execute within is defined by all of the settings in the [Lucee Admin](https://rorylaitila.gitbooks.io/lucee/content/lucee_admin.html). However, each code base can define its own Application.cfc [Component](https://rorylaitila.gitbooks.io/lucee/content/classes.html) file. Code bases should always define an Application.cfc

##A Basic Application
Any application is defined by simply the presense of an Application.cfc file in the webroot. Consider the following structure:

* /wwwroot
  * Application.cfc
  * index.cfm


{% gist id="https://gist.github.com/roryl/fed1716562c197feb32bd1fc1ef6c1da",file="Application.cfc" %}{% endgist %}

{% gist id="https://gist.github.com/roryl/fed1716562c197feb32bd1fc1ef6c1da",file="index.cfm" %}{% endgist %}
