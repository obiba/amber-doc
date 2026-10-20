.. _item_map_location:

Map Location
============

The ``geo`` format renders a map on which a point, a line or a polygon is drawn: the value is a `GeoJSON <https://datatracker.ietf.org/doc/html/rfc7946>`__ geometry.

``format: "geo"`` (or ``geojson``) on an object property, in the schema or in the ``options`` of the control, displays a map. The data is a GeoJSON geometry in WGS84 longitude / latitude: ``{ "type": "Point", "coordinates": [lon, lat] }``, a ``LineString`` (an array of positions) or a ``Polygon`` (an array of rings, each closed on its first position). The coordinates are rounded to ``options.precision`` decimals (6 by default, about 10 cm).

The kinds of geometry the control accepts come from ``options.geometries``, any subset of ``point``, ``linestring`` (or ``line``) and ``polygon``, all three by default; a ``type`` property with an ``enum`` of GeoJSON types in the schema restricts them too. When several kinds are allowed, the toolbar selects the one to draw. Click the map to place a point, or to add the points of a line or a polygon, double click to finish; a vertex can then be dragged, and drawing again replaces the value. **My position** uses the Geolocation API of the browser: for a point it writes the current position, for a line or a polygon it centers the map on it (the button is not displayed when the API is unavailable, ``options.locate: false`` hides it). **Clear** removes the value.

The map is built with `OpenLayers <https://openlayers.org/>`__, loaded on demand the first time a geo control is displayed. The tiles are those of OpenStreetMap by default, with their attribution under the map: ``options.tiles`` (a ``{z}/{x}/{y}`` URL template, or ``{ url, attributions }``) selects another source. The tiles are displayed in a scale of greys (inverted in dark mode) so that the geometry stands out, ``options.grayscale: false`` keeps their colors. The initial view fits the value, else ``options.center`` (``[lon, lat]``) and ``options.zoom`` (12 by default with a center; a zoom alone applies to the world view).

``options.feature: true`` stores the geometry wrapped in a GeoJSON Feature, ``{ "type": "Feature", "geometry": {...}, "properties": null }``; a Feature value is read whatever the option. Several features are a `list <https://www.obiba.org/quasar-json-form/#/controls/list>`__ of geo items: ``{ "type": "array", "items": { "type": "object", "format": "geo" } }``.

Point
~~~~~

When a point is allowed, latitude and longitude inputs under the map show the value and accept one typed in (``options.inputs: false`` hides them). The map fits the point once both are valid.

Line and polygon
~~~~~~~~~~~~~~~~

``options.minPoints`` and ``options.maxPoints`` bound the number of points of a line or a polygon while drawing. The number of points of the value is displayed under the map.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================ ======================================= =======================
Entry            Schema                                  UI schema
================ ======================================= =======================
**Map location** ``{"type": "object", "format": "geo"}`` ``{"type": "Control"}``
================ ======================================= =======================

Schema
------

The schema shapes that select this renderer:

========================================= =======================================================================================================
Schema                                    Description
========================================= =======================================================================================================
``{ "type": "object", "format": "geo" }`` A GeoJSON geometry drawn on a map; ``geojson`` is accepted too, in the schema or as ``options.format``.
========================================= =======================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============== ================ ================= ===============================================================================================================================================================================================================================================================================================================================================
Setting        Type             Default           Description
============== ================ ================= ===============================================================================================================================================================================================================================================================================================================================================
``format``     String                             ``geo`` (or ``geojson``), also accepted as the schema ``format``.
``geometries`` Array \| String  ``all``           Kinds of geometry the control accepts, among ``point``, ``linestring`` (or ``line``) and ``polygon``, as an array or a comma separated string. A ``type`` property with an ``enum`` of GeoJSON types in the schema restricts them too. With several kinds, the toolbar selects the one to draw. Values: ``point``, ``linestring``, ``polygon``.
``tiles``      String \| Object ``OpenStreetMap`` Tile source of the map: a ``{z}/{x}/{y}`` URL template, or ``{ url, attributions }`` with the attributions (markdown) displayed under the map. Defaults to ``config.geo.tiles``, then the OpenStreetMap standard tiles.
``center``     Array                              ``[lon, lat]`` center of the initial view when there is no value (defaults to ``config.geo.center``, then a world view).
``zoom``       Number                             Zoom of the initial view when there is no value (defaults to ``config.geo.zoom``, then 12 with a ``center``); without a ``center``, the zoom of the world view.
``height``     Number \| String ``320``           Height of the map, in px when a number (defaults to ``config.geo.height``).
``color``      String           ``primary``       Quasar color (or any CSS color) of the drawn geometry and of the selected draw mode.
``feature``    Boolean          ``false``         Store the geometry wrapped in a GeoJSON ``Feature`` (``{ type: "Feature", geometry, properties: null }``). A ``Feature`` value is read whatever this option. For several features, use a `list <https://www.obiba.org/quasar-json-form/#/controls/list>`__ of geo items.
``precision``  Number           ``6``             Number of decimals of the coordinates (defaults to ``config.geo.precision``).
``minPoints``  Number                             Minimum number of points of a line or a polygon being drawn.
``maxPoints``  Number                             Maximum number of points of a line or a polygon being drawn (the drawing finishes when reached).
``inputs``     Boolean          ``true``          Show latitude and longitude inputs under the map when a point is allowed, to display and type the value.
``grayscale``  Boolean          ``true``          Display the tiles in a scale of greys (inverted in dark mode), the geometry keeping its color; ``false`` keeps the colors of the tiles (defaults to ``config.geo.grayscale``).
``locate``     Boolean          ``true``          Show the **My position** button (only when the Geolocation API is available): for a point it writes the current position, for a line or a polygon it centers the map on it.
============== ================ ================= ===============================================================================================================================================================================================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

============ ================== =======================================
Check        Message key        Description
============ ================== =======================================
``required`` ``error.required`` A required control with no value (AJV).
============ ================== =======================================

Data
----

A GeoJSON geometry in WGS84 longitude / latitude: ``Point``, ``LineString`` or ``Polygon`` (rings closed on their first position), or a ``Feature`` of one with ``feature: true``, or no value. Drawing replaces the current geometry, **Clear** removes it. Read-only, the map can be browsed but not edited; a hidden control (``rules.visible``) loses its value; a value that is not a valid geometry is displayed as nothing and left untouched until the user acts.

.. code:: json

   { "location": { "type": "Point", "coordinates": [-73.5673, 45.5017] } }

See also the `Map Location <https://www.obiba.org/quasar-json-form/#/controls/geo>`__ page of the Quasar JSON Form documentation, with live examples.
