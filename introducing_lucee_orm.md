

## Lucee ORM example


Lucee ORM manages persistence through objects, which are also called entities in the ORM context. In Lucee, persistence is managed through CFCs and their properties. Each persistent CFC in Lucee application maps to a table in the database. Each property in the persistent CFC maps to a column in the table.

The following example explains these concepts by building a simple application, which would enable you to jumpstart with Lucee ORM. The example uses the cfartgallery data source that is shipped as part of Lucee 9 documentation option in the installer. The cfartgallery data source has Artists and Art tables. Artists has a one-to-many relationship with the Art table.

**Step 1:**

Specify the ORM settings in the Application.cfc file.

The minimum required settings are mentioned in the following sample code snippet:

Application.cfc

```
this.name = "ArtGalleryApp";
this.ormenabled = "true";
this.datasource = "cfartgallery"; 
```

Apart from these, there are other settings that you can use to configure ORM. For details, see [ORM settings](WS2CED8D4C-8F3B-4f88-AEAA-D3F94F04964D.html).

Important: Define these setting only in Application.cfc and not in Application.cfm.

**Step 2:**

Map the ARTISTS.cfc to the database table.

1.  Create the ARTISTS.cfc.

2.  Flag it as a persistent CFC and map it to the ARTISTS table.

    To make the ARTISTS.cfc persistent, the persistent attribute should be set to true in the cfcomponent tag. The table attribute should be set to the table name. If table attribute is not specified, then the CFC name is taken as the table name.

    Each CFC can be given an entity name. Entity name is the name used by the ORM related functions to work with the persistent CFC. It can be specified by using the entityname attribute in cfcomponent. If entityname is not specified, then the CFC name is taken as the entityname.

3.  Now, create properties in ARTISTS.cfc and map them to the columns in the table. One property should be created for each column in the table. To map the property to the column, the column attribute should be set to the corresponding column name. If the column attribute is not specified, then the name of the property is taken as the column name.

For details on setting the ORM-specific attributes, see [Define ORM mapping](WS53C28604-E798-4175-97AE-D7BDF124056C.html).

The ARTISTS.cfc is defined as follows:

```
component persistent="true" {
    property name="id" column = "ARTISTID" generator="increment";
    property name="FIRSTNAME"; 
    property name="LASTNAME"; 
    property name="ADDRESS"; 
    property name="CITY"; 
    property name="STATE"; 
    property name="POSTALCODE"; 
    property name="EMAIL"; 
    property name="PHONE"; 
    property name="FAX"; 
    property name="thepassword"; 
}
```

**Step 3:**

Perform CRUD operations.

To retrieve data from the ARTISTS table, use EntityLoad():

```
ARTISTS = EntityLoad("ARTISTS");
```

All the records from the ARTISTS table are retrieved as an object array.

To add a new artist, create a new artist object and call EntitySave() for this object.

```
try { 
    newArtistObj = EntityNew("artists"); 
    newArtistObj.setfirstname("John"); 
    newArtistObj.setlastname("Smith"); 
    newArtistObj.setaddress("5 Newport lane"); 
    newArtistObj.setcity("San Francisco"); 
    newArtistObj.setstate("CA"); 
    newArtistObj.setPostalCode("90012"); 
    newArtistObj.setphone("612-832-2343"); 
    newArtistObj.setfax("612-832-2344"); 
    newArtistObj.setemail("jsmith@company.com"); 
    newArtistObj.setThePassword("jsmith"); 
    EntitySave(newartistobj); 
    ormflush(); 
} catch(Exception ex) { 
    WriteOutput("#ex.message#"); 
} 
}
```

To update an existing record, load that object and make changes to it. Lucee automatically detects that the row for this object needs to be updated and it will get updated when ORMFlush() is called.

>Note: ORMFlush() is called at the end of the request by default.

In the following code, the new ArtistObj is already managed by ORM, so it does not need to be loaded again.

```
newArtistObj.setphone("612-832-1111"); 
ormflush();
```

To delete a record, EntityDelete() is used.

```
EntityDelete(newArtistObj); 
ormflush();
```

**Step 4:**

Define Relationships

First define the mapping for the ART table to define a relationship between artwork and artists.

The ART.cfc is defined as follows:

```
component persistent="true" {
    property name="artid" generator="increment";
    property name="artname"; 
    property name="price"; 
    property name="largeimage"; 
    property name="mediaid"; 
    property name="issold"; 
}
```

In cfartgallery, the table ARTISTS has a one-to-many relationship with ART table, which are joined using the foreign key column ARTISTID. This means that each artist has created multiple artwork pieces and many artworks are created by one artist. To represent this in the object model, each ARTISTS object would contain an array of ART objects. Each ART object will contain a reference to its ARTISTS object. This is an example of a bidirectional relationship.

To achieve this, you need to add an extra property to the ARTISTS.cfc object that contains the array of ART objects for that ARTIST.

```
property name="art" type="array" fieldtype="one-to-many" cfc="Art" fkcolumn="ARTISTID"
```

fieldtype="one-to-many" specifies the type of relation.

CFC="Art" is used to convey that the relationship is with "ART" cfc.

fkcolumn="artistid" specifies the foreign key.

ART forms a many-to-one relationship with ARTISTS table because each piece of artwork is created by an artist and many other pieces of artwork are created by the same artist. To define this relationship, add a property in ART.cfc to define the relationship with ARTISTS.cfc.

```
property name="artists" fieldtype="many-to-one" fkcolumn="artistid" cfc="Artists" lazy="true"
```

fieldtype="many-to-one" specifies the type of relation.

CFC="ARTISTS" is used to convey that the relationship is with "ARTISTS" cfc.

fkcolumn="ARTISTID" specifies the foreign key.

**Step 5:**

Retrieve records in relationship

```
artist = EntityLoad("Artists", 1, true); 
arts = artist.getArts(); 
WriteOutput("<b>" & artist.getid() & " " & artist.getfirstname() & " " & 
artist.getlastname() & "</b> has " & ArrayLen(arts) & " arts:<br>"); 
if (ArrayLen(arts) > 0) 
{ 
    for(j = 1; j <= ArrayLen(arts); j ++) 
    { 
        art = arts[j]; 
        WriteOutput(art.getartname() & "<br>"); 
    } 
} 
```

Adapted from http://help.adobe.com/en_US/ColdFusion/9.0/Developing/WSD628ADC4-A5F7-4079-99E0-FD725BE9B4BD.html