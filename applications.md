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

If running this code, we'll see:

![](basic_application.png)

##Naming an Application
Its possible for there to be more than one Application.cfc defined for a particular website, or even particular server. Lucee keeps track of Application settings based on providing a unique Application name. Each Application in a server using this name, will have access to the same [Application Scope](https://rorylaitila.gitbooks.io/lucee/content/lifecycle_scopes.html#application)

To name an application, define `this.name = "myapp";` in the Application.cfc, like so:

{% gist id="https://gist.github.com/roryl/00fb4e5a51b3b904b954b03537198594",file="Application.cfc" %}{% endgist %}

##Application Settings
All configurable application settings are defined in the implicit component constructor area along with the Application name. There are many dozens of settings to control all aspects of the Lucee runtime. Below is just an example of a settings, which sets the timezone for the application:

{% gist id="https://gist.github.com/roryl/51c9c9a54fd672ff1bb8e1f597ac8234",file="Application.cfc" %}{% endgist %}

See more details about [Application Settings](https://rorylaitila.gitbooks.io/lucee/content/applicationcfc_settings.html) in the Developing Application section.