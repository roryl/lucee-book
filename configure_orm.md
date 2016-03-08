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
 
