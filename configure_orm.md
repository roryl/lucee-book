# Configure ORM

The configuration for ORM is done in Application.cfc which makes this configuration application specific. For a ColdFusion application to use ORM, the following are the mandatory settings that need to be configured:

1. Enable ORM for the application. To do this, set the ormenabled property to true in the THIS scope of application.cfc

2. Provide the data source name by either setting data source property to true in the THIS scope of application or by defining it in ORM configuration for the application.
Note that the data source should be configured on the server.

The ORM configuration is specified using a struct called ormsettings, which is defined in the THIS scope of Application.cfc. The following table describes the settings for ORM that can be defined in Application.cfc.

| Property Name | Description |
| -- | -- |
| ormenabled | Specifies whether ORM should be used for the ColdFusion application.Set the value to true to use ORM. The default is false. |
| datasource | Defines the data source that should be used by ORM.|
|ormsettings | The struct that defines all the ORM settings. For details, see ORM settings |


## ORM settings

The following settings can be set in the ormsettings struct that ColdFusion uses to configure ORM. All these settings are optional. If you specify the value of any ORM setting to true or yes, then the setting is enabled, otherwise it is disabled.

# Configure ORM

The configuration for ORM is done in Application.cfc which makes this configuration application specific. For a Lucee application to use ORM, the following are the mandatory settings that need to be configured:

1. Enable ORM for the application. To do this, set the ormenabled property to true in the THIS scope of application.cfc

2. Provide the data source name by either setting data source property to true in the THIS scope of application or by defining it in ORM configuration for the application.
Note that the data source should be configured on the server.

The ORM configuration is specified using a struct called ormsettings, which is defined in the THIS scope of Application.cfc. The following table describes the settings for ORM that can be defined in Application.cfc.

| Property Name | Description |
| -- | -- |
| ormenabled | Specifies whether ORM should be used for the Lucee application.Set the value to true to use ORM. The default is false. |
| datasource | Defines the data source that should be used by ORM.|
|ormsettings | The struct that defines all the ORM settings. For details, see ORM settings |


## ORM settings

The following settings can be set in the ormsettings struct that Lucee uses to configure ORM. All these settings are optional. If you specify the value of any ORM setting to true or yes, then the setting is enabled, otherwise it is disabled.

<table border="1" cellpadding="4" cellspacing="0">

<thead align="left">

<tr>

<th valign="top" width="NaN%" id="d17e53969">

Property Name

</th>

<th valign="top" width="NaN%" id="d17e53972">

Default

</th>

<th valign="top" width="NaN%" id="d17e53975">

Description

</th>

</tr>

</thead>

<tbody>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

autogenmap

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

true

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether Lucee should automatically generate mapping for the persistent CFCs. If autogenmap=false, mapping should be provided in the form of .HBMXML files.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

automanageSession

Added in Lucee 9.0.1

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

true

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Lets you specify if Lucee must manage Hibernate session automatically.

<div class="para">

*   If enabled: Lucee manages the session completely. That is, it decides when to flush the session, when to clear the session, and when to close the session.

*   If disabled: The application is responsible for managing flushing, clearing, or closing of the session. The only exception is (in the case of transaction), when the transaction commits, the application flushes the session.

Lucee closes the ORM session at the end of request irrespective of this flag being enabled or disabled.</div>

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

cacheconfig

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the location of the configuration file that should be used by the secondary cache provider.This setting is used only when secondarycacheenabled=true.

See [Secondary level cache](WSf01dbd23413dda0e54af3c7912012f78097-7ff0.html) for details.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

cacheprovider

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

ehcache

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the cache provider that should be used by ORM as secondary cache. The values can be:

<div class="para">

*   Ehcache

*   JBossCache

*   Hashtable

*   SwarmCache

*   OSCache

Fully qualified name of the class for any other cache provider.</div>

This setting is used only when secondarycacheenabled=true.

See [Secondary level cache](WSf01dbd23413dda0e54af3c7912012f78097-7ff0.html) for details.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

catalog

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the default Catalog that should be used by ORM.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

cfclocation

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the directory (or array of directories) that should be used by Lucee to search for persistent CFCs to generate the mapping. If cfclocation is set, Lucee looks at only the paths specified in it. If it is not set, Lucee looks at the application directory, its sub-directories, and its mapped directories to search for persistent CFCs.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

datasource

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the data source that should be used by ORM. If it is not specified here, then the data source specified for the application is picked up. Use the following convention to specify a datasource name: this.datasource="<datasource_name>";

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

dbcreate

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

none

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

<div class="para">Lucee ORM can automatically create the tables for your application in the database when ORM is initialized for the application. This can be enabled by using dbcreate in ormsettings. dbCreate takes the following values:

*   update: Setting this value creates the table if it does not exist or update the table if it exists.

*   dropcreate: Setting this value drops the table if it exists and then creates it.

*   none (default): Setting this value does not change anything in the database schema.

</div>

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

dialect

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the dialect.

<div class="para">Lucee supports the following dialects:

*   DB2

*   DB2AS400

*   DB2OS390

*   Derby

*   PostgreSQL

*   MySQL

*   MySQLwithInnoDB

*   MySQLwithMyISAM

*   Oracle8i

*   Oracle9i

*   Oracle10g

*   Sybase

*   SybaseAnywhere

*   MicrosoftSQLServer

*   Informix

</div>

Apart from these dialects, you can specify custom dialects by using the fully qualified class name.

<div class="para">

<div class="note"><span class="notetitle">Note:</span> For Microsoft Access, dialect cannot be detected automatically. Use Microsoft SQL Server as the dialect for it.</div>

</div>

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

eventHandling

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

false

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether ORM Event callbacks should be given. See [Event Handling in CFC](WSA5D7AC9C-A395-48ac-BBD3-35F6A4B21715.html) for details.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

flushatrequestend

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

true

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether ormflush should be called automatically at request end. If <samp class="codeph">flushatrequestend is false, <samp class="codeph">ormflush is not called automatically at request end.

See [ORM session management](WS00180FBE-6DE0-43f0-84CB-DCE04A9FCCA4.html).

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

logSQL

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

false

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether the SQL queries that are executed by ORM will be logged. If LogSQL=true, the SQL queries are logged to the console.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

namingstrategy

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Defines database standard and naming convention. See [Naming strategy](WS57BC54E4-4AED-4f11-9E15-B26DF1B7DF09.html).

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

ormconfig

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

The Hibernate configuration file.

This file contains various configuration parameters like, dialect, cache settings, and mapping files that are required for the application. For more details, see [www.hibernate.org/hib_docs/reference/en/html/session-configuration.html](http://www.hibernate.org/hib_docs/reference/en/html/session-configuration.html).

The settings defined in the ormsettings override the settings defined in the Hibernate Configuration XML file.The connection information in the Hibernate Configuration XML file is however ignored because Lucee uses its own connection pool.

You will need to use this only when you need to use a hibernate setting that is not available using ormsetting.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

savemapping

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

false

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether the generated Hibernate mapping file has to be saved to disc. If you set the value to true, the Hibernate mapping XML file is saved with the filename "CFC name".hbmxml in the same directory as the CFC.

If any value of savemapping is specified in CFC, it will override the value specified in the ormsetting.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

schema

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies the default Schema that should be used by ORM.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

secondarycacheenabled

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

false

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether secondary caching should be enabled. See [Use secondary cache](WS4C3B91C4-E209-4449-B1EE-E44F4F5D3D14.html) for details.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

skipCFCWithError

Added in Lucee 9.0.1

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

false

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Lets you specify if Lucee must skip the CFCs that have errors. If set to true, Lucee ignores the CFCs that have errors.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

sqlscript

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Path to the SQL script file that gets executed after ORM is initialized. This applies if dbcreate is set to <samp class="codeph">dropcreate. This must be the absolute file path or the path relative to the application.The SQL script file lets you populate the tables before the application is accessed.

</td>

</tr>

<tr>

<td valign="top" width="NaN%" headers="d17e53969 ">

useDBForMapping

</td>

<td valign="top" width="NaN%" headers="d17e53972 ">

true

</td>

<td valign="top" width="NaN%" headers="d17e53975 ">

Specifies whether the database has to be inspected to identify the missing information required to generate the Hibernate mapping. The database is inspected to get the column data type, primary key and foreign key information.

</td>

</tr>

</tbody>

</table>
 
 
 Adapted from http://help.adobe.com/en_US/ColdFusion/9.0/Developing/WSD628ADC4-A5F7-4079-99E0-FD725BE9B4BD.html

 
