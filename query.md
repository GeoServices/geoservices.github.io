---
layout: default
---

{::options parse_block_html="true" /}

<div class="col-lg-3">
## Query

* [Formats](#formats)
* [Filter by Attributes](#filter-by-attributes)
* [Filter by Location](#filter-by-location)
* [Aggregation Statistics](#aggregation-statistics)

</div>
<div class="col-lg-9">

Layers have a single endpoint for requesting features. The `/query` supports filtering by attributes, geography, time, as well as aggregate statistics.

### Defaults

To request all the data, up to the maximum record count, you need to provide a few required parameters:

`.../FeatureServer/0/query?where=1=1&outFields=*&f=json`

This request states: "Return all the features all the attributes as JSON."

<hr>
## Formats

GeoServices support a few common formats. Most commonly these are `html` and `json` and depending on the version of Service can include `geojson`, `kml`, and `amf`. Format outputs are requested by using the URI parameter `f={format}`. `html` is the default response.

`.../Education_WebMercator/MapServer/5?f=json`

<hr>
## Filter by Attributes


### Examples

Total number of students by school type and number of zipcodes that have this school type:
<pre>
http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5/query
  ?where=FACUSE like 'Elementary School' AND ZIP_CODE=20002 AND STATUS='Active'
  &amp;outFields=*
  &amp;f=json
</pre>

<a href="http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5/query?where=FACUSE='Elementary+School'+AND+ZIP_CODE=20002+AND+STATUS='Active'&outFields=*&f=json" target="_new">See API Response</a>

### Parameters

| Parameter     | Description           | Example  |
| ------------- |-------------| -----|
| where  | SQL-like string of boolean operators | FACUSE like 'Elementary' AND ZIP_CODE=20002 |

<hr>

## Filter by Location

### Example

Single point location:

<pre>http://tigerweb.geo.census.gov/arcgis/rest/services/TIGERweb/Places_CouSub_ConCity_SubMCD/MapServer/15/query
    ?outFields=*
    &amp;geometryType=esriGeometryPoint
    &amp;geometry=-77.06930,38.89733
    &amp;inSR=4326
    &amp;f=json</pre>

Extent area:

<pre>
http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5/query
?where=FACUSE like '%Elementary%' AND TOTAL_STUD >= 200 AND TOTAL_STUD <= 1000
&amp;geometry={"xmin":-77.0036,"ymin":38.8879,"xmax":-76.98434,"ymax":38.90007,"spatialReference":{"wkid":4326}}
&amp;geometryType=esriGeometryEnvelope
&amp;inSR=4326
&amp;outFields=*
</pre>


### Parameters

| Parameter     | Description           | Example  |
| ------------- |-------------| -----|
| geometryType  | Point, Line or Polygon request | `esriGeometryPoint` |
| geometry      | Longitude, Latitude pair or JSON   |   `-77.06930,38.89733` |
| inSR          | Spatial reference of input geometry | `4326` |


<hr>
## Aggregation Statistics

### Examples

Total number of students by school type and number of zipcodes that have this school type:
<pre>
http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5/query
  ?groupByFieldsForStatistics=FACUSE,
  &amp;outStatistics= [{
        "statisticType": "sum", 
        "onStatisticField": "TOTAL_STUD", 
        "outStatisticFieldName": "TOTAL_STUD_SUM"
      },{
        "statisticType": "count", 
        "onStatisticField": "ZIP_CODE", 
        "outStatisticFieldName": "ZIP_CODE_COUNT"
      }]
  &amp;where=1=1
  &amp;outFields=*
  &amp;f=json
</pre>

<a href='http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5/query?groupByFieldsForStatistics=FACUSE&outStatistics=[{"statisticType": "sum", "onStatisticField": "TOTAL_STUD", "outStatisticFieldName": "TOTAL_STUD_SUM"},{"statisticType": "count", "onStatisticField": "ZIP_CODE", "outStatisticFieldName": "ZIP_CODE_COUNT"}]&where=1=1&outFields=*&f=json' target="_new">See API Response</a>

### Parameters

| Parameter     | Description           | Example  |
| ------------- |-------------| -----|
| groupByFieldsForStatistics  | Attribute to use as key for aggregation | `ZIP_CODE` |
| outStatistics      | Array of statistics calculations. Can be one or many   | `[{"statisticType": "sum", "onStatisticField": "TOTAL_STUD", "outStatisticFieldName": "TOTAL_STUD_SUM"}]` |
| outStatistics.statisticType | Type of Statistic to calculate: `count`,`sum`, `avg`, `var`, `max`, `min` | `sum` |
| outStatistics.onStatisticField | Layer attribute to use with statistic type | `NUM_STUDENTS` |
| outStatistics.outStatisticFieldName | Name to use for the field | `NUM_STUDENTS_SUM` |

</div>

