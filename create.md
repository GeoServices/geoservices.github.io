---
layout: default
---

{::options parse_block_html="true" /}

<div class="col-lg-3">


</div>

<div class="col-lg-9">

Geoservices are composed of two important aspects: Services and Layers.

By analogy, a Service is like a database and a Layer is like a Table. A Service will have one or many Layers. A Layer has many Features, which are like Rows.

## Authentication

An access token is required for creating a service.

`POST https://www.arcgis.com/sharing/rest/tokens/generateToken`

- `f=json`
- `username={username}`
- `password={password}`
- `expiration={time in minutes}`


## Creating a Service

To create a Layer, you will first need to create a Service, and then you can add Layers.

`POST https://www.arcgis.com/sharing/rest/content/users/{username}/createService`

- `outputType=featureService`
- `createParameters={'name':'ExampleService'}`
- `f=json`
- `token=...`

### Response

<pre>
{
  "encodedServiceURL": "http://services.arcgis.com/bkrWlSKcjUDFDtgw/arcgis/rest/services/ExampleService/FeatureServer",
  "itemId": "cfda...",
  "name": "ExampleService",
  "serviceItemId": "cfda...",
  "serviceurl": "http://services.arcgis.com/bkrWlSKcjUDFDtgw/arcgis/rest/services/ExampleService/FeatureServer",
  "size": -1,
  "success": true,
  "type": "Feature Service",
  "isView": false
}
</pre>

For more details, see the [Create Service API Documentation](http://resources.arcgis.com/en/help/arcgis-rest-api/index.html#/Create_Service/02r30000027r000000/)


## Creating a Layer

A Layer requires a schema, defined as `fields`.

To create a layer, you need to call `addToDefinition` in the the `rest/admin/services` for your Service.

`POST {serviceurl}/addToDefinition`

The `serviceurl` was returned in the API `createService`. You can also build the URL: `POST https://services.arcgis.com/{orgId}/arcgis/rest/admin/services/{ServiceName}/FeatureServer/addToDefinition`

- `addToDefinition=...` _see Layer definition below_
- `async=true`
- `f=json`
- `token=...`

### Fields

First, a layer requires a schema for Fields. A Field includes `name`, `type`, `alias`, and other database parameters.

A Field of type `esriFieldTypeOID` is required for storage and indexing.

- `name` - column name, cannot contain spaces or special punctuation
- `alias` - human-readable name
- `type` - one of `esriFieldTypeString`, `esriFieldTypeDouble`, `esriFieldTypeInt`

An example Field JSON:

<pre>
[{
  "name": "OBJECTID",
  "alias": "OBJECTID",
  "type": "esriFieldTypeOID",
  "sqlType": "sqlTypeOther",
  "nullable": false,
  "editable": false,
  "domain": null,
  "defaultValue": null
},{
  "name": "ExampleSField",
  "alias": "An Example String Field",
  "nullable": true,
  "editable": true,
  "domain": null,
  "defaultValue": null,
  "type": "esriFieldTypeString",
  "sqlType": "sqlTypeNVarchar",
  "length": 256
},{
  "name": "ExampleDField",
  "alias": "An Example Double Field",
  "nullable": true,
  "editable": true,
  "domain": null,
  "defaultValue": null,
  "type": "esriFieldTypeDouble",
  "sqlType": "sqlTypeDecimal",
  "length": 256
},{
  "name": "ExampleIField",
  "alias": "An Example Integer Field",
  "type": "esriFieldTypeInteger",
  "actualType": "int",
  "sqlType": "sqlTypeInteger",
  "nullable": true,
  "editable": true,
  "domain": null,
  "defaultValue": null
},{
  "name": "ExampleDateField",
  "alias": "An Example Date Field",
  "type": "esriFieldTypeDate",
  "sqlType": "sqlTypeOther",
  "length": 8,
  "nullable": true,
  "editable": false,
  "domain": null,
  "defaultValue": null
}]
</pre>

This JSON is contained in the full `layers: []` definition below.

### Layer definition

The full layer definition is:

<pre>
{
  "layers": [
    {
      "adminLayerInfo": {
        "geometryField": {
          "name": "Shape",
          "srid": 4326
        }
      },
      "name": "ExampleLayer",
      "type": "Feature Layer",
      "displayField": "",
      "description": "",
      "copyrightText": "",
      "defaultVisibility": true,
      "relationships": [

      ],
      "isDataVersioned": false,
      "supportsRollbackOnFailureParameter": true,
      "supportsAdvancedQueries": true,
      "geometryType": "esriGeometryPoint",
      "minScale": 0,
      "maxScale": 0,
      "extent": {
        "type": "extent",
        "xmin": -8591193.021457616,
        "ymin": 4686637.938322677,
        "xmax": -8560023.564035526,
        "ymax": 4726686.262985074,
        "spatialReference": {
          "wkid": 102100
        }
      },
      "drawingInfo": {
        "transparency": 0,
        "labelingInfo": null,
        "renderer": {
          "type": "simple",
          "symbol": {
            "color": [
              20,
              158,
              206,
              130
            ],
            "size": 18,
            "angle": 0,
            "xoffset": 0,
            "yoffset": 0,
            "type": "esriSMS",
            "style": "esriSMSCircle",
            "outline": {
              "color": [
                255,
                255,
                255,
                220
              ],
              "width": 2.25,
              "type": "esriSLS",
              "style": "esriSLSSolid"
            }
          }
        }
      },
      "allowGeometryUpdates": true,
      "hasAttachments": true,
      "htmlPopupType": "esriServerHTMLPopupTypenull",
      "hasM": false,
      "hasZ": false,
      "objectIdField": "OBJECTID",
      "globalIdField": "",
      "typeIdField": "",
      "fields": fields,
      "indexes": [

      ],
      "types": [

      ],
      "templates": [
        {
          "name": "New Feature",
          "description": "",
          "drawingTool": "esriFeatureEditToolPoint",
          "prototype": {
            "attributes": {
              "Name": null,
              "Integer": 0,
              "Date": "2016-12-22T02:34:51.768Z"
            }
          }
        }
      ],
      "supportedQueryFormats": "JSON",
      "hasStaticData": false,
      "maxRecordCount": 1000,
      "capabilities": "Query,Editing,Create,Update,Delete"
    }
  ]
}
</pre>

For more details, see the [Add to Definition API Documentation](http://resources.arcgis.com/en/help/arcgis-rest-api/index.html#/Add_to_Definition_Feature_Layer/02r300000228000000/)



</div>


## SQL types

sqlType is needed in feature service to bind to the actual field in the dbase during query or even editing.

SqlType also allows the client to control how the column is created in the database.


| SqlType | FieldType | Result database column type | Notes |
| ------- | --------- | ------ | ------- |
| Not relevant | esriFieldTypeBlob | Column size determine the varbinary size created. Default is max.  [varbinary]|
| Not relevant | esriFieldTypeDate |  [datetime2] – default [smalldatetime] – column size = 4  [datetimeoffset] – column size = 10 |
| Not relevant | esriFieldTypeDouble | [float] | |
| Not relevant | esriFieldTypeSingle | [real]  | |
| Not relevant | esriFieldTypeOID | [int] | |
| Not relevant | esriFieldTypeGlobalId esriFieldTypeGUID | [uniqueidentifier] | |
| sqlTypeBigInt | esriFieldTypeInteger | [bigint] | |
| sqlTypeInteger | esriFieldTypeInteger | [int] | |
| sqlTypeBit | esriFieldTypeSmallInteger | [bit] | |
| sqlTypeTinyInt | esriFieldTypeSmallInteger | [tinyint] | |
| sqlTypeInteger | esriFieldTypeSmallInteger | [smallint] | |
| Not relevant | esriFieldTypeString | [nvarchar] | Column size determines the max nvarchar.  Default is [nvarchar] (max) |
| sqlTypeTime | esriFieldTypeString | [time] | |
| sqlTypeTimestamp | esriFieldTypeString | [timestamp2] | |
