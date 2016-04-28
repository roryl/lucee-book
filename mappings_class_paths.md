# Mappings (Class Paths)

By default, all instances of Lucee Components and Templates are located starting from the webroot of the application. Mappings are used typically used to locate files outside of the webroot

Take for example the following directory structure

* /
  * /core
    * include.cfm
    * basicComponent.cfc
  * /web
    * /subfolder
      * view.cfm
    * Application.cfc
    * index.cfm
  

In this example, the web server is running from the /web directory, and therefore /core/include.cfm can not be browsed directly from a browser.

<script src="https://gist-it.appspot.com/github/roryl/lucee-mappings/blob/master/web/Application.cfc"></script>