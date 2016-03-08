# Introducing Lucee ORM

In traditional applications, database access was achieved by:

* Managing relational data using tags such as cfquery, cfinsert, and cfupdate, which handle SQL statements.
* Managing objects using Lucee components (CFCs), and object lifecycle using the application itself
* Writing SQL queries for each CFC, even for basic CRUD (Create, Retrieve, Update, and Delete) operations.
* The complexity of managing these tasks increases as your application grows.


Lucee ORM automates most of these tasks, which:

* Makes application code cleaner and more manageable
* Enhances your productivity and lets you develop database applications faster
* Creates applications that can run faster because of built-in ORM optimizations
* Minimizes the amount of code you write
* Apart from providing a framework for mapping the object model with the relational database, Lucee ORM provides data query and retrieval facilities.

For more information, see www.hibernate.org.

Lucee ORM example

Lucee ORM manages persistence through objects, which are also called entities in the ORM context. In Lucee, persistence is managed through CFCs and their properties. Each persistent CFC in Lucee application maps to a table in the database. Each property in the persistent CFC maps to a column in the table.

The following example explains these concepts by building a simple application, which would enable you to jumpstart with Lucee ORM.

Step 1:

Specify the ORM settings in the Application.cfc file.

The minimum required settings are mentioned in the following sample code snippet:

Application.cfc

```
this.name = "ArtGalleryApp"; 
this.ormenabled = "true";
this.datasource = "artgallery";
```