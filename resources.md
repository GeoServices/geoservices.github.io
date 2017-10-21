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
<code>http://{host}/{site}/rest/services/{folder}/{serviceName?}/{serviceType}/{layerIndex?}/{operation?}</code>

Where `{resource}` is a path placeholder for for a value, and `{resource?}` is optional path value.
</p>


<p>For example the layer "DC Public Schools" has the URI address of: <a href="http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5" title="DC Public Schools service">http://maps2.dcgis.dc.gov/dcgis/rest/services/DCGIS_DATA/Education_WebMercator/MapServer/5</a>

	<ul>
		<li><code>{host} = maps2.dcgis.dc.gov</code></li>
		<li><code>{site} = dcgis</code></li>
		<li><code>{folder} = DCGIS_DATA</code></li>
		<li><code>{serviceName} = Education_WebMercator</code></li>
		<li><code>{serviceType} = MapServer</code></li>
		<li><code>{layerIndex} = 5</code></li>
		<li><code>{operation}</code> is not used in this example</li>
	</ul>
</p>

<h3> Terminology</h3>

When using the GeoService API, there are a few common terms. These terms closely match a typical database structure. 

<dl>
<dt>Server</dt> 

<dd>a web server that connects a database and provides many services. </dd>

<dt>Folder</dt> 
<dd>a collection of Services organized by a topic.</dd>

<dt>Service</dt>
<dd>a high-level container of many layers, <em>e.g. Education</em>. Similar to a <em>Database</em>. A server has many layers like a database has many tables. A Service is often a thematic grouping of layers. </dd>

<dt>Service Type</dt>
<dd>specifies if the data layer is vector (points/lines/polygons) or raster (pixels/image). Examples include `FeatureServer`, `MapServer`, `ImageServer`</dd>

<dt>Layer</dt>

<dd>a collection of data that have a common schema, <em>e.g. Public Schools in DC</em>. Similar to a <em>database table</em>. Layers are addressed as their `layerIndex`, starting at 0. A Layer has many features. <em>aka Dataset</em></dd>

<dt>Feature</dt> 

<dd>an individual location, <em>e.g. a School</em>. Similar to a <em>database row</em> or <em>database record</em>. A Feature has a geometry and many attributes.</dd>

<dt>Attribute</dt> 
<dd>an aspect of a feature, <em>e.g. Number of Students</em>. Similar to a <em>database column</em>. An attribute can be a string, number, timestamp, id, or blob. </dd>
</dl>
</div>