# Architecture

In Lucee ORM, you need to define an object mapping to create persistent objects. The object mapping includes details such as:

*   The table name for the object's class

*   The column name that corresponds to each field in the object

*   The join conditions for related objects

Lucee allows you to specify the mapping in CFCs. Such CFCs are called as persistent CFCs. Each persistent CFC usually maps to a table in the database. Each property in the CFC usually maps to a column in the table. Additional properties may be used to define relationships and other mapping details.

When Lucee creates the Hibernate configuration for the application, these persistent CFCs are used to automatically generate Hibernate mapping files, which have the extension ".hbmxml". For example, if ARTISTS.cfc is a persistent CFC, Lucee would automatically generate Artists.hbmxml. Hibernate mapping files contain the mapping information in XML format that Hibernate defines, to work with Lucee ORM. These Hibernate mapping files can be created manually.

For more information about creating Hibernate mappings manually, see [Advanced mapping](WS027D3772-2E98-4d5b-8800-054A62EBF8D9.html).

To use Lucee ORM, Lucee application must have ormenabled set to true in the THIS scope of Application.cfc. To define a persistent CFC, set persistent="true" in cfcomponent tag. An array of attributes are available in cfcomponent and cfproperty to specify mapping information.

For details, see [Define ORM mapping](WS53C28604-E798-4175-97AE-D7BDF124056C.html).

When the application starts, Lucee first loads the Hibernate configuration file if it is specified in the application. The Hibernate configuration file contains various configuration parameters like including, dialect, cache settings, and mapping files that are required for the application. If a configuration file is not specified, Lucee ORM creates the Hibernate configuration using the default settings.

For details about these configuration parameters, see [www.hibernate.org/hib_docs/reference/en/html/session-configuration.html](http://www.hibernate.org/hib_docs/reference/en/html/session-configuration.html).

After loading the Hibernate configuration, all the mapping files (*.hbmxml) in the application folder and its mapped folders are loaded and added to the configuration.

Lucee then searches for persistent CFCs in the application folder and its mapped folders. If the hibernate mapping file is not present for any persistent CFC, Lucee generates it. If mapping information, such as primary key, foreign key, and column data type is missing in the persistent CFCs, Lucee automatically inspects the database and identifies the mapping.

Lucee then checks if DDL needs to be generated. This can be configured using the dbcreate option in the ORM settings. Based on the configuration option specified in dbcreate, tables are created or updated.The Hibernate SessionFactory is then built and made available to the application as long as the application is running. The SessionFactory is used to create Hibernate sessions that manage the persistent object lifecycle.

In Lucee, a Hibernate session starts when the first CRUD method is called and ends when the request ends or when the ORMCloseSession() method is called.

To improve performance, Hibernate batches all the Create/Update/Delete operations in the session and runs them when the session is flushed or only when necessary. Session Flush happens when the request ends or when the ORMFlush() method is called.

For transactions, a new session is always created at the start of a transaction and ends at the end of a transaction. Any previous open sessions are flushed and closed at the start of the transaction.

The Hibernate configuration is created and loaded only when the application starts. Therefore, any modifications to the mapping in the persistent CFCs or in the Hibernate mapping files are not loaded automatically. To load these modifications, you can either restart the application or call ORMReload().

To restart the application, you can stop the application using ApplicationStop() and the next request to any page in this application automatically starts it.

