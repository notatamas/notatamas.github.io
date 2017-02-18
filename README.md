# FOSS IOW GIS

This project is created as an academic assignment for the SDI Module on CU. The website incorporates a number of proprietary and free GIS mapping solutions.

The site is created to present a prototype website to showcase the possible transformation from the currently used proprietary web mapping tools used by the IoW Council to free and open-source alternatives.

## Approach

The site generation is implemented in <a href="https://jekyllrb.com/">Jekyll</a>. The layout is generated with the <a href="http://shopify.github.io/liquid/">Liquid</a> template language. Hosted on <a href="https://pages.github.com/">Github Pages</a>,
 the layout is based on <a href="http://getbootstrap.com/">Bootstrap</a>
 and <a href="https://jquery.com/">jQuery</a>
 and inspired by the <a href="https://startbootstrap.com/template-overviews/clean-blog/">Clean blog</a> Bootstrap theme by <a href="http://davidmiller.io/">David Miller</a>.</p>

#### Maps as a collection
Each map is stored in a Jekyll Collection, therefore the pages presenting the various maps are created using for loops, such as:

```
{% for map in site.maps %}
    {% map.sample_content %}
{% endfor %}
```

#### Map variables
The maps have several variables that are utilized later. An important variable is the map type, that can be either "current" or "proposed".

An example of using this variable is as follows:
```
{% assign current_map = site.maps | where:"type","current" %}
{% for map in current_map limit:3 %}
    {% include map_list.html %}
{% endfor %}
```

Another example is the use of Bootstrap Popovers to show information about the maps in the map list at a glance by hovering above the picture.
```HTML
<a href="{{ map.url }}" data-toggle="popover" data-html="true" data-trigger="hover" data-placement="top"
data-content="<b>Map type:</b> {{ map.application }} <br />
<b>Layer(s):</b> {{ map.layer }} <br />
<b>Base layer:</b> {{ map.base_layer }} <br />
<b>Description:</b> {{ map.purpose }}" title="Map details"><img src="{{ site.baseurl }}/img/{{ map.img }}" alt="{{ map.title }}"></a>
```

#### Global variables
The site also makes use of Jekyll "global" variables, and stores them in the config file. Later these variables are used as:

```
{{ site.gm_api_key }}
```
This way the Google maps API key can be referenced from every page of the site.

#### Modular html files
The site is created with modular design approach, therefore to avoid repetition, the common elements are included in the following way:

```
{% include secure_warning.html %}
```
An example of this is the following warning:

![alt text](http://i.imgur.com/OpbdGdJ.png "Toggle buttons")



#### Custom functions

A set of custom functions were implemented to control layers from Google Maps and OpenLayers.
This includes toggle buttons:

![alt text](http://i.imgur.com/XDkDPtA.png "Toggle buttons")

```Javascript
function toggleLayers(layer, div) {
if (layer.getMap() == map) {
layer.setMap(null);
document.getElementById(div).className += "btn btn-default";
} else {
layer.setMap(map);
document.getElementById(div).className += "btn btn-default active";
}
}
```
Controlled by the buttons:
```HTML
<div class="row" style="margin-bottom:20px">
    <button id="mastPylonButton" type="button" class="btn btn-default active" onclick="toggleLayers(mastpylon, this.id);">Toggle masts and pylons</button>
    <button id="elecSubButton" type="button" class="btn btn-default active" onclick="toggleLayers(elsubstation, this.id);">Toggle electricity sub stations</button>
    <button id="elecPoleButton" type="button" class="btn btn-default active" onclick="toggleLayers(elpoles, this.id);">Toggle electricity poles</button>
</div>
```

And buttons to control layer opacity:

![alt text](http://i.imgur.com/ZmvV1HU.png "Toggle buttons")

The buttons can be controlled via the Javascript functions:

```Javascript
// Increasing layer opacity. Should be assigned to a button
function increaseLayerOpacity(layer) {
console.log(layer.getOpacity());
	if (layer.getOpacity()<0.91) {
		layer.setOpacity(layer.getOpacity() + 0.1);
console.log(layer.getOpacity());
}
}

// Decreasing layer opacity. Should be assigned to a button
function decreaseLayerOpacity(layer) {
console.log(layer.getOpacity());
	if (layer.getOpacity()>0.09) {
		layer.setOpacity(layer.getOpacity() - 0.1);
console.log(layer.getOpacity());
}
}
```

And the functions are called by the HTML elements:
```HTML
<strong>Flood area opacity:</strong>
<button type="button" class="btn btn-default" onclick="increaseLayerOpacity(flood);">+</button>
<button type="button" class="btn btn-default" onclick="decreaseLayerOpacity(flood);">-</button>
```

## Used mapping tools and base layer providers

Proprietary tools used:
* ESRI ArcGIS Online
* ArcGIS Web App
* ESRI server

Free tools:
* Google maps
* CartoDb
* ArcGIS JS API
* MapBox
* Bing Maps

Open-Source tools:
* OpenLayers
* LeafletJS
* OpenStreetMap


## Site structure
#### Home
The home page intends to present the project and to show a give a short introduction about the current  state of web mapping tools used by the Isle of Wight. In addition the general assumptions of the proposed web mapping solutions is explained.

![alt text](http://i.imgur.com/st7qBlJ.png "Toggle buttons")

#### Current maps
The current maps page shows a list of the current maps.
![alt text](http://i.imgur.com/Q70cHu0.png "Toggle buttons")

#### Proposed maps
The proposed maps page shows a list of the proposed maps to the Isle of Wight Council in the same layout as the current maps page.

#### Tourist maps
The tourist map page shows a proposed image map for the Isle of Wight with tourist information. The destinations are presented with Bootstrap Modals.
![alt text](http://i.imgur.com/yVzwTDO.png "Toggle buttons")

#### Filter
The filter page shows the current and proposed maps categorized by the layer data source and the used web mapping technology.
![alt text](http://i.imgur.com/GQFWawk.png "Toggle buttons")

## Warning
Modern browsers do not allow HTTP requests in sites using HTTPS.
Since Github pages uses HTTPS and the CU server uses HTTP, some requests are blocked.
To overcome this issue, the following approach is suggested:

Start Google Chrome with allowed insecure content:

On \*nix systems:
```
google-chrome --allow-running-insecure-content
```
On Windows:
```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --allow-running-insecure-content
```
Please make sure to close every chrome instance before, otherwise chrome will just start a new tab in the current session.


## To examine the project locally:
* Clone or download the repository
* Install Ruby and Jekyll
* Cd into the folder
* Start the server with 'jekyll serve --watch'
* Navigate to 127.0.0.1:4000


## License

MIT license.
