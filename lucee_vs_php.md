# Lucee vs PHP

Like PHP, Lucee is a dynamically typed language that is compiled or interpreted in another language (PHP compiles to C, Lucee to Java). Lucee is an Object Oriented language with classes, a large standard library and an included templating langage. Templates in Lucee are similar to classic PHP conventions of using page includes, although popular templating engines like Handlebars is available for Lucee. 

One of the main differences between Lucee and PHP is each request by default in PHP spawns a new process and dies at the end of the request, freeing up those resources. In order to have persistent memory, other services have to be configured along side PHP for PHP to put and get data from. Lucee on the other hand runs on the Java Virtual Machine (JVM) and each request runs within the running Java web server that Lucee ties into. This means that Lucee contains persistent data collections useful for your application, and the JVM handles garbage collection of old requests and data.

Lucee and PHP share a common history in that their languages are some of the oldest and continually used web languages today. The Lucee language is based on CFML which was created by Allaire in 1995, around the same time as PHP.

PHP and Lucee both share the C Language syntax family.