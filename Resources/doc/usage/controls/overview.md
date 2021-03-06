# Overview map control

The overview map control displays a thumbnail overview map reflecting the current map viewport within a wider area. 
This control appears by default in the bottom right corner of the map, and is by default shown in its collapsed state.

## Build your overview map control

### By configuration file

By default, the bundle doesn't need any configuration. Most of the service have a default configuration which allows you to use the given objects like they are.
The ``ivory_google_map.overview_map_control`` service is. The configuration describes below is this default configuration.

```
# app/config/config.yml

ivory_google_map:
    overview_map_control:
        # TRUE if the overview map control is opened else FALSE
        opened: false
```

``` php
<?php

// Requests the ivory google map overview control service
$overviewMapControl = $this->get('ivory_google_map.overview_map_control');
```

### By coding

``` php
<?php

// Requests the ivory google map overview control service
$overviewMapControl = $this->get('ivory_google_map.overview_map_control');

// Configure your overview map control
$overviewMapControl->setOpened(false);
```

## Add your overview map control to the map

``` php
<?php

// Requests the ivory google map overview control service
$overviewMapControl = $this->get('ivory_google_map.overview_map_control');

// Add your overview map control to the map
$map->setOverviewMapControl($overviewMapControl);
$map->setOverviewMapControl(false);
```
