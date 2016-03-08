# Scaffolding

Scaffolding refers to how you structure your files for your application. Building modern web applications is complex and every application is different. Lucee does not impose on you how to structure your application, like say Ruby on Rails. It allows more flexibility for unique situaitons. However for Lucee, there tends to be a common set of conventions that are used when building web applications. This chapter discusses common structures for your application that are likely to meet your needs with Lucee.

Unless you are building a command line application with Lucee using CommandBox, the standard application with Lucee is a Web Application. This scaffolding section deals only with Web Applications. 

##Basic Web App
Your Lucee web application will live in a webroot on a web server. At its most basic level, the webroot must contain an index.cfm that will process the request as the default template, and an Application.cfc to define your application. 

- wwwroot
  - /assets - JS & CSS files
  - /views - other Lucee templates (.cfm)
  - Application.cfc
  - Index.cfm

For the most basic types of web applications, which may be single purpose, only have one or two features, or may be used for prototyping, this kind of structure above may be appropriate. You can also use the above for learning and experimentation without having to deal with also learning one of the below frameworks. 

If you start adding many features, the above structure may not be enough to handle all of your needs and you should consider learning one of the frameworks below to structure your code. 


##Using Frameworks
In Lucee there are a few major open source MVC (Model-View-Contorller) frameworks that are suitable for most web applications. 

###[Framework 1 (fw/1)](https://github.com/framework-one/fw1)
A lightweight MVC framework, best for do it yourself people who only want the minimal of structure.

###[CFWheels](http://cfwheels.org/)
A MVC framework inspired by Ruby On Rails, to develop quickly with a ton of baked in features

###[ColdBox](https://www.coldbox.org/)
A full featured MVC platform suitable for small to enterprise applications, with great documentation and a vibrant ecosystem


##Custom Scaffolding
If your needs are complex or your use case does not follow the capabilities of those frameworks, then there is a common way to structure your application in Lucee that takes into account some scenarios and conventions.

Here is a possible complex directory structure:

- /root
  - /model - Entities & Value Objects of your Domain
  - /services - Communicates with other domains
  - /vendor - Third party code
  - /util - Non domain / universal code
  - /app - client web application    
    - /controllers - CFCs to route requests to the Model
    - /views - Lucee Templates containing HTML
    - /layouts - Lucee Templates containing global layout HTML
    - wwwroot - This is where your website is served from
      - /assets - CSS/JS/Images
      - Application.cfc - Your Application file
      - Index.cfm - Default page view

The purpose of this structure is not so much that you must adhere to it exactly, but it is an example to recommend some larger points regarding developing with Lucee. These points apply to most web applications as well.

This scaffolding assumes a [Domain-Driven-Design](https://en.wikipedia.org/wiki/Domain-driven_design) & Object-Oriented style of development, which is common for consumer and business web applications. 

###Separate out the "app" from your "model"
In the above structure, our "app" contains the code which represents our client (a HTML web application), while the code in the "root" is our core domain model. The root represents all of the core components, libraries, services and third party code necessary to create your application. By separating out the client "app" from the "root" it more easily allows you to separate concerns. This may allow you to even have multiple types of client apps, like a REST API, a mobile app, and a website, which all use the common root.

###Keep your Web Root (wwwroot) separate from your core files
In Lucee you *can* put all of your files in the webroot, but it is not recommended. Only publically accessible assets like JS, CSS and image files should be in the webroot, along with the primary Application.cfc and index.cfm. This keeps your application's other templates and components secure from being directly accessed and simplifies your security. 






