.. _item_image_map:

Image Map
=========

The ``image-map`` format renders the values of a `selection <https://www.obiba.org/quasar-json-form/#/controls/select>`__ as clickable areas of one image: click an area to select its value.

The image is the ``options.image`` of the control: an http(s) or relative URL or a data URI, in JPEG, PNG or WebP, or ``{ src, width, height }`` when its natural size is known up front. Each value needs an area, given as the ``area`` key of its ``oneOf`` entry, or in the ``options.areas`` map (required for a plain ``enum``, and winning over the entries). An area follows the HTML ``<area>`` convention: ``{ shape, coords }`` with ``rect`` (``x1, y1, x2, y2``), ``circle`` (``cx, cy, r``) or ``poly`` (``x1, y1, x2, y2, ...``), the coords in the pixels of the image, as an array or a comma separated string. A value without a valid area is only available in the list.

The areas are drawn as an SVG overlay that scales with the image (the parts outside of the image are not drawn), so it can be constrained with ``options.maxWidth`` and still fit its container. The ``title`` of the entry is the tooltip and the accessible name of the area. An image that cannot be loaded shows a placeholder icon.

Single choice
~~~~~~~~~~~~~

``options.format: "image-map"`` on a string with ``enum`` or ``oneOf`` selects one value. A hovered area is tinted, a selected one is filled and outlined in the ``color`` option (``primary`` by default). A second click clears an optional choice.

A `select <https://www.obiba.org/quasar-json-form/#/controls/select>`__ under the image shows the same value: choosing an entry in the list highlights its area, and clicking an area updates the list. ``options.select: false`` hides it, the error and the hint are then displayed under the image. ``options.outline: true`` outlines all the areas, to show where they are.

Multiple choices
~~~~~~~~~~~~~~~~

On an array with ``uniqueItems`` and ``enum`` or ``oneOf`` items, the data is an array of the selected values, empty when nothing is selected, in the order of the entries. Once ``maxItems`` values are selected, the other areas are disabled. The list shows the values as chips.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

============= ==================================================================================================================== ========================================================================
Entry         Schema                                                                                                               UI schema
============= ==================================================================================================================== ========================================================================
**Image map** ``{"type": "string", "oneOf": [{"const": "a", "title": "A", "area": {"shape": "rect", "coords": [0, 0, 50, 50]}}]}`` ``{"type": "Control", "options": {"format": "image-map", "image": ""}}``
============= ==================================================================================================================== ========================================================================

Schema
------

The schema shapes that select this renderer:

================================================================================================== =====================================================================================================
Schema                                                                                             Description
================================================================================================== =====================================================================================================
``{ "type": "string", "enum": [...] } + format: "image-map"``                                      One area per ``enum`` value, the areas come from ``options.areas``.
``{ "oneOf": [{ "const", "title", "area" }] } + format: "image-map"``                              One area per ``oneOf`` entry, its ``area`` key is the shape (``rules.visible`` on an entry hides it).
``{ "type": "array", "uniqueItems": true, "items": { "enum" \| "oneOf" } } + format: "image-map"`` Multiple choices, the data is an array.
================================================================================================== =====================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============ ================ =========== =======================================================================================================================================================================================================================================================================================
Setting      Type             Default     Description
============ ================ =========== =======================================================================================================================================================================================================================================================================================
``format``   String                       ``image-map``, also accepted as the schema ``format``.
``image``    String \| Object             The image: a URL, or ``{ src, width, height }`` with its natural size in pixels (read from the loaded image otherwise). JPEG, PNG and WebP, as an http(s) or relative URL or a data URI.
``areas``    Object                       Area of each value, keyed by value: ``{ shape, coords }``. Wins over the ``area`` of the ``oneOf`` entry.
``area``     Object                       On a ``oneOf`` entry or an ``areas`` entry: ``shape`` is ``rect``, ``circle`` or ``poly``, ``coords`` are ``x1, y1, x2, y2`` / ``cx, cy, r`` / ``x1, y1, x2, y2, ...`` in the pixels of the image, as an array of numbers or a comma separated string (the HTML ``<area>`` convention).
``select``   Boolean          ``true``    Show a select of the same values under the image, in sync with the areas; the other options (``dense``, ``outlined``...) are passed to it. Without it, the error and the hint are displayed under the image.
``maxWidth`` Number \| String             Maximum width of the image, in px when a number; the image otherwise fills its container.
``color``    String           ``primary`` Quasar color of the hovered and selected areas.
``outline``  Boolean          ``false``   Outline all the areas, not only the hovered and selected ones.
============ ================ =========== =======================================================================================================================================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

============ ================== ======================================================================================================
Check        Message key        Description
============ ================== ======================================================================================================
``required`` ``error.required`` A required single choice with no value (AJV).
``minItems`` ``error.minItems`` Lower bound of a multiple choice (AJV).
``maxItems`` ``error.maxItems`` Upper bound of a multiple choice (AJV); the renderer also disables the other areas once it is reached.
============ ================== ======================================================================================================

Data
----

The selected value, or an array of values for a multiple choice (an empty array when nothing is selected). A second click clears an optional single choice; once ``maxItems`` values are selected, the other areas are disabled. Read-only, the selection is displayed but ignores clicks; a hidden control (``rules.visible``) loses its value, a value that is no longer an entry is cleared. The areas are focusable, Space or Enter toggles them.

.. code:: json

   { "room": "kitchen", "rooms": ["kitchen", "pool"] }

See also the `Image Map <https://www.obiba.org/quasar-json-form/#/controls/image-map>`__ page of the Quasar JSON Form documentation, with live examples.
