.. _item_images:

Images
======

The ``images`` format renders the values of a `selection <https://www.obiba.org/quasar-json-form/#/controls/select>`__ as images laid out on a grid: click one to select it.

Each value needs an image, given as the ``image`` key of its ``oneOf`` entry, or in the ``options.images`` map of the control (required for a plain ``enum``, and winning over the entries). An image is an http(s) or relative URL, or a data URI, in JPEG, PNG or WebP. The ``title`` of the entry is the caption and the alternative text, translated with ``t()``. An image that cannot be loaded, or a data URI of another type, shows a placeholder icon.

Single choice
~~~~~~~~~~~~~

``options.format: "images"`` on a string with ``enum`` or ``oneOf`` selects one value. A selected image is outlined and badged in the ``color`` option (``primary`` by default). A second click clears an optional choice.

Multiple choices
~~~~~~~~~~~~~~~~

On an array with ``uniqueItems`` and ``enum`` or ``oneOf`` items, the data is an array of the selected values, empty when nothing is selected, in the order of the entries. Once ``maxItems`` values are selected, the other images are disabled.

With ``options.ordering: true`` the array keeps the click order instead: the badge shows the rank and buttons under the caption move an image before or after the other selected ones.

Grid
~~~~

The images fill a CSS grid, as many columns as fit ``options.minWidth`` (120px) by default. ``options.columns`` and ``gap`` take the values of a `grid layout <https://www.obiba.org/quasar-json-form/#/layouts/grid>`__: a number of columns, a track list, or a Quasar breakpoint map (``{ xs: 2, md: 4 }``). An entry (or an ``options.images`` entry) can carry a ``grid`` placement (``column``, ``row``, ``colSpan``, ``rowSpan``, ``area``) to span cells or be placed explicitly. ``captions: false`` hides the captions, ``ratio`` and ``fit`` shape the images.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========== ======================================================================================================================= ========================================================
Entry      Schema                                                                                                                  UI schema
========== ======================================================================================================================= ========================================================
**Images** ``{"type": "string", "oneOf": [{"const": "a", "title": "A", "image": ""}, {"const": "b", "title": "B", "image": ""}]}`` ``{"type": "Control", "options": {"format": "images"}}``
========== ======================================================================================================================= ========================================================

Schema
------

The schema shapes that select this renderer:

=============================================================================================== =====================================================================================================
Schema                                                                                          Description
=============================================================================================== =====================================================================================================
``{ "type": "string", "enum": [...] } + format: "images"``                                      One image per ``enum`` value, the images come from ``options.images``.
``{ "oneOf": [{ "const", "title", "image" }] } + format: "images"``                             One image per ``oneOf`` entry, its ``image`` key is the URL (``rules.visible`` on an entry hides it).
``{ "type": "array", "uniqueItems": true, "items": { "enum" \| "oneOf" } } + format: "images"`` Multiple choices, the data is an array.
=============================================================================================== =====================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============ ========================== =========== =================================================================================================================================================================================================================================================================
Setting      Type                       Default     Description
============ ========================== =========== =================================================================================================================================================================================================================================================================
``format``   String                                 ``images``, also accepted as the schema ``format``.
``images``   Object                                 Image of each value, keyed by value: a URL, or ``{ src, grid, title }``. Wins over the ``image`` / ``grid`` / ``title`` of the ``oneOf`` entry. JPEG, PNG and WebP, as an http(s) or relative URL or a data URI.
``columns``  Number \| String \| Object             ``grid-template-columns``: a number of equal columns, a track list, or a breakpoint map (``{ xs: 2, md: 4 }``). By default as many columns of ``minWidth`` as fit (``repeat(auto-fill, minmax(minWidth, 1fr))``).
``minWidth`` Number \| String           ``120px``   Minimum width of a column when ``columns`` is not set.
``gap``      Number \| String \| Object ``10``      Row and column gap, in px when a number; ``rowGap`` / ``columnGap`` win over it.
``grid``     Object                                 On a ``oneOf`` entry or an ``images`` entry: the placement of its cell, ``column`` / ``row`` (``2``, ``"1 / 3"``, ``"span 2"``), ``colSpan`` / ``rowSpan``, ``area``, as an element of a `grid layout <https://www.obiba.org/quasar-json-form/#/layouts/grid>`__.
``ratio``    Number \| String           ``1``       Aspect ratio of the images (``QImg`` ``ratio``), ``16/9``, ``4/3``...
``fit``      String                     ``cover``   ``object-fit`` of the images: ``cover``, ``contain``, ``fill``, ``scale-down``, ``none``.
``loading``  String                     ``lazy``    ``loading`` attribute of the images: ``lazy`` or ``eager``.
``captions`` Boolean                    ``true``    Show the caption (the entry ``title``, or the value) under each image.
``color``    String                     ``primary`` Quasar color of the outline, badge and move buttons of a selected image.
``ordering`` Boolean                    ``false``   Multiple choices: keep the click order, show the rank in the badge and the move buttons under the caption. Otherwise the array follows the order of the entries.
============ ========================== =========== =================================================================================================================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

============ ================== =======================================================================================================
Check        Message key        Description
============ ================== =======================================================================================================
``required`` ``error.required`` A required single choice with no value (AJV).
``minItems`` ``error.minItems`` Lower bound of a multiple choice (AJV).
``maxItems`` ``error.maxItems`` Upper bound of a multiple choice (AJV); the renderer also disables the other images once it is reached.
============ ================== =======================================================================================================

Data
----

The selected value, or an array of values for a multiple choice (an empty array when nothing is selected). A second click clears an optional single choice; once ``maxItems`` values (or the ``max`` rule, which wins) are selected, the other images are disabled. Read-only, the selection is displayed but ignores clicks; a hidden control (``rules.visible``) loses its value, a value that is no longer an entry is cleared. The tiles are focusable, Space or Enter toggles them.

.. code:: json

   { "landscape": "forest", "places": ["forest", "lake"] }

See also the `Images <https://www.obiba.org/quasar-json-form/#/controls/images>`__ page of the Quasar JSON Form documentation, with live examples.
