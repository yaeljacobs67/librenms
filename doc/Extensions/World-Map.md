source: Extensions/World-Map.md
# World Map Configuration

LibreNMS comes with a configurable Geo Map based on World Map Widget to visualize where your equipment is located geographically.

### World Map Widget

World Map Widget, requires you to have properly formatted addresses in sysLocation or sysLocation override. As part of the standard poller these addresses will be Geocoded by Google and stored in the database.

Location resolution happens as follows

 1. If `device['location']` contains `[lat, lng]` (note the square brackets), that is used
 1. If there is a location overide for the device in the WebUI and it contains `[lat, lng]` (note the square brackets), that is used.
 1. Attempt to resolve lat, lng using `$config['geoloc']['engine']`
 1. Properly formatted addresses in sysLocation or sysLocation override, under device settings.

Example:

[40.424521, -86.912755]

or

1100 Congress Ave, Austin, TX 78701


We have two current mapping engines available:

- Leaflet (default)
- Jquery-Mapael


### World Map Widget Settings

- *Initial Latitude / Longitude*: The map will be centered on those coordinates.
- *Initial Zoom*: Initial zoom of the map. [More information about zoom levels](https://wiki.openstreetmap.org/wiki/Zoom_levels).
- *Grouping radius*: Markers are grouped by area. This value define the maximum size of grouping areas.
- *Show devices*: Show devices based on there status.

Example Settings:

![Example World Map Settings](/img/world-map-widget-settings.png)


### Offline OpenStreet Map
If you can't access OpenStreet map directly you can run a local [tile server](http://wiki.openstreetmap.org/wiki/Tile_servers). To specify a different url you can set:

```php
$config['leaflet']['tile_url'] = 'localhost.com';
```

### Jquery-Mapael config
Further custom options are available to load different maps of the world, set default coordinates of where the map will zoom and the zoom level by default. An example of
this is:

```php
$config['map']['engine']                                = "jquery-mapael";
$config['mapael']['default_map'] = 'mapael-maps/united_kingdom/united_kingdom.js';
$config['mapael']['map_width'] = 400;
$config['mapael']['default_lat'] = '50.898482';
$config['mapael']['default_lng'] = '-3.401402';
$config['mapael']['default_zoom'] = 20;
```

A list of maps can be found in ```html/js/maps/``` or ```html/js/mapael-maps/```.
