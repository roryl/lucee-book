# ORM Migrations
Keeping SQL database tables and columns in sync with the code without any downtown is a very common problem with databases. Lucee has built in data model versioning which can make transitioning from one version of the data model to another much easier.

##The Problem
Often in an application, new features are going to be added which both need to be reflected in the deloyed code, and in the database simultaneously. Consider for example a simple application which has two models, customer and order:

In version 1 of the application, the order class has a function `getTotalCost()`, whose implementation simply returns the value of the field total_cost. However, a new feature request comes in which says "total cost should be the total_cost minus any discounts".

Now the order class needs a new field, discount, and getTotalCost() needs to be updated to reflect subtracting the discount. However, if we deploy the new version of the code without the database change, the code will fail due to the missing columns.


