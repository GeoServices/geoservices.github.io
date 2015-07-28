---
layout: page
title: Resources
---
<div class="col-lg-2">
&nbsp;
</div>
<div class="col-lg-9">
<h3>Resources</h3>

<p>It's useful to understand the common terminology and resources that compose the GeoServices API.</p>


<h3>URI structure</h3>

<p>The GeoServices REST API follows a common structure. 
</p>
<code>http://{host}/{site}/rest/services/{folder}/{serviceName}/{serviceType}/{layerIndex}</code>

<p>For example the layer "DC Public Schools" has the URI address of: http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5
</p>


<dl>
<dt>Server</dt> 
<dd>a web server that connects a database and provides many services.</dd>
<dt>Folder</dt> 
<dd>a collection of Services organized by a topic.</dd>

<dt>Service</dt> a high-level container of many layers, _e.g. Education_. A Service is often a thematic grouping of ldters. Examples include `FeatureServer`, `MapServer`, `ImageServer`</dd>

<dt>Layer</dt>
<dd>a collection of data that have a common schema, _e.g. Public Schools in DC_. Layers are addressed as their index, starting at 0. A Layer has many features. <em>aka Dataset</em></dd>

<dt>Feature</dt> 
<dd>an individual location, <em>e.g. a School</em>. A Feature has a geometry and many attributes.</dd>

<dt>Attribute</dt> 
<dd>an aspect of a feature, <em>e.g. Number of Students</em>. An attribute can be a string, number, timestamp, id, or blob. </dd>
</dl>
</div>