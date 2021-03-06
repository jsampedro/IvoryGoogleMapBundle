# Events

JavaScript within the browser is event driven, meaning that JavaScript responds to interactions by generating events, and expects a program to listen to interesting events. 
The event model for the Google Maps API V3 is similar to that used in V2 of the API, though much has changed under the hood. There are two types of events:

- User events (such as "click" mouse events) are propagated from the DOM to the Google Maps API. These events are separate and distinct from standard DOM events.
- MVC state change notifications reflect changes in Maps API objects and are named using a property_changed convention

## Build your event

### By configuration file

By default, the bundle doesn't need any configuration. Most of the service have a default configuration which allows you to use the given objects like they are.
The ``ivory_google_map.event`` service is. The configuration describes below is this default configuration.

```
# app/config/config.yml

ivory_google_map:
    event:
        # Prefix used for the generation of the event javascript variable
        prefix_javascript_variable: "event_"
```

``` php
<?php

// Requests the ivory google map event service
$event = $this->get('ivory_google_map.event');
```

The configuration file allows you to manage the generated javascript variable. 
All the other configuration can only be done by coding.

### By coding

``` php
<?php

// Requests the ivory google map event service
$event = $this->get('ivory_google_map.event');

// Configure your event
$event->setInstance($instance);
$event->setEventName($eventName);
$event->setHandle($handle);

// It can only be used with a DOM event
// By default, the capture flag is false
$event->setCapture(true);
```

#### Instance

The ``$instance`` variable describes the javascript variable which registers the event. 
Each Ivory google map objects which can register an event have a method called ``getJavascriptVariable`` which identifies this variable.

For example, in the case of an info window, it can be:

``` php
<?php

$instance = $infoWindow->getJavascriptVariable();
```

#### Event name

Each object has his own event name which are described in the google map documentation.

#### Handle

The ``$handle`` is the javascript function which is executed when the event is triggered.

For example, it can be:

``` php
<?php

$handle = 'function(){alert("The event has been triggered");}'
```

## Add your event to the map

The map wraps an event manager which allows you to add events. Like describes in the introduction, two differents type of event can be used.

### DOM event

``` php
<?php

// Add a DOM event
$map->getEventManager()->addDomEvent($event);

// Add a DOM event which will be triggered only one time 
$map->getEventManager()->addDomEventOnce($event);
```

### MVC event

``` php
<?php

// Add an event
$map->getEventManager()->addEvent($event);

// Add an event which will be triggered only one time
$map->getEventManager()->addEventOnce($event);
```
