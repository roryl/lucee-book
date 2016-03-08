# Scaffolding

Scaffolding refers to how you structure your files for your application. Building modern web applications is complex and every application is different. However for Lucee and platforms like it, there tends to be a common set of conventions that are used when building web applications. This chapter discusses common structures for your application that are suitable for use with Lucee.

Unless you are building a command line application with Lucee using CommandBox, the standard application with Lucee is a Web Application. This scaffolding section deals only with Web Applications. 

##Basic Web App
Your Lucee web application will live in a webroot on a server. At its most basic level, the webroot must contain an index.cfm that will process the request as the default template, and an Application.cfc to define your application. 

- wwwroot
  - /assets - JS & CSS files
  - /views
  - Application.cfc
  - Index.cfm

For your most basic types of web applications, which may be single purpose, only have one or two features, or may be used for prototyping, this kind of structure above may be appropriate. You can also use the above for learning and experimentation without having to deal with also learning one of the below frameworks. 

If you start adding many features, the above structure may not be enough to handle all of your needs and you should consider learning one of the frameworks below to structure your code. 


##Using Frameworks
In Lucee there are a few major open source MVC (Model-View-Contorller) frameworks that are suitable for most web applications. 

###[Framework 1 (fw/1)](https://github.com/framework-one/fw1)
A lightweight MVC, best for do it yourself people who only want the minimal of structure

###[CFWheels](http://cfwheels.org/)
A MVC framework inspired by Ruby On Rails, to develop quickly with a ton of baked in features

###[ColdBox](https://www.coldbox.org/)
A full featured MVC platform suitable for small to enterprise applications, with great documentation and a vibrant ecosystem


##Custom Scaffold
If your needs are complex or your use case does not follow the capabilities of those frameworks, then there is a common way to structure your application in Lucee that takes into account some scenarios and conventions.

Here is a possible complex directory structure:

- /root
  - /model - Entities & Value Objects of your Domain
  - /services - Communicates with other Domains
  - /vendor - Third party code
  - /util - Non domain / universal code
  - /app - Public web application
    - /assets - CSS/JS/Images
    - /controllers - CFCs to route requests to the Model & Services
    - /views - Lucee Templates containing HTML
    - /layouts - Lucee Templates containing global layout HTML
    - wwwroot - This is where your website is served from
      - Application.cfc - Your Application file
      - Index.cfm - Default page view

The purpose of this structure is not so much that you must adhere to it exactly, but it is an example to recommend some larger points regarding developing with Lucee. These points apply to most web applications as well.

This scaffolding assumes a [Domain-Driven-Design](https://en.wikipedia.org/wiki/Domain-driven_design) & Object-Oriented style of development, which is common for consumer and business web applications. 

###Separate out the "app" from your "model"


###Keep your Web Root (wwwroot) separate from your core files






