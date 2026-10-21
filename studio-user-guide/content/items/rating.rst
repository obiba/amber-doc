.. _item_rating:

Rating
======

An integer with ``options.format: "rating"`` renders a `QRating <https://quasar.dev/vue-components/rating>`__.

The schema ``title`` and ``description`` are displayed above the rating and the ``hint`` of the control element under it, unless there is an error. Every other option is passed to ``QRating``: ``max``, ``icon``, ``iconSelected``, ``color``, ``size``, ``noReset``... ``max`` defaults to the schema ``maximum``.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========== =================================================== ========================================================
Entry      Schema                                              UI schema
========== =================================================== ========================================================
**Rating** ``{"type": "integer", "minimum": 0, "maximum": 5}`` ``{"type": "Control", "options": {"format": "rating"}}``
========== =================================================== ========================================================

Schema
------

The schema shapes that select this renderer:

==================================================== ======================================================
Schema                                               Description
==================================================== ======================================================
``{ "type": "integer" } + options.format: "rating"`` An integer property with the ``rating`` format option.
==================================================== ======================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

========= ====== ========================== =============================================================================================================================================================================================================
Setting   Type   Default                    Description
========= ====== ========================== =============================================================================================================================================================================================================
``max``   Number ``schema maximum, else 5`` Number of icons.
``icon``  String                            Icon name (Quasar icon set).
``color`` String                            Quasar color of the icons.
``size``  String                            Size of the icons, a CSS unit (``2em``) or a Quasar size (``md``).
Other     any                               Every option is passed as a prop to `QRating <https://quasar.dev/vue-components/rating#qrating-api>`__: ``max``, ``icon``, ``iconSelected``, ``iconHalf``, ``color``, ``size``, ``noReset``, ``noDimming``...
========= ====== ========================== =============================================================================================================================================================================================================

Data
----

An integer; no value displays no selected icon.

.. code:: json

   { "stars": 4 }

See also the `Rating <https://www.obiba.org/quasar-json-form/#/controls/rating>`__ page of the Quasar JSON Form documentation, with live examples.
