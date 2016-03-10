# Mappings (Class Paths)

By default, all instances of Lucee Components and Templates are resolved, starting from the webroot of your application. In order for Lucee to find a Component that you are instantiating, or a Template that you are including, it must be able to get to them. 

Take for example the following directory structure

* /myApp
  * Application.cfc
  * index.cfm
  * /views
    * myOtherTemplate.cfm



getDirectoryFromPath(getCurrentTemplatePath())