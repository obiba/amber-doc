.. _item_slider:

Slider
======

An integer with ``options.format: "slider"`` renders a `QSlider <https://quasar.dev/vue-components/slider>`__.

The schema ``title`` and ``description`` are displayed above the slider and the ``hint`` of the control element under it, unless there is an error. Every other option is passed to ``QSlider``: ``min``, ``max``, ``step``, ``markers``, ``label``, ``labelAlways``, ``color``... ``min`` and ``max`` default to the schema ``minimum`` and ``maximum``. To select two ends, see the `range <https://www.obiba.org/quasar-json-form/#/controls/range>`__.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========== ==================================================== ========================================================
Entry      Schema                                               UI schema
========== ==================================================== ========================================================
**Slider** ``{"type": "integer", "minimum": 0, "maximum": 10}`` ``{"type": "Control", "options": {"format": "slider"}}``
========== ==================================================== ========================================================

Schema
------

The schema shapes that select this renderer:

==================================================== ======================================================
Schema                                               Description
==================================================== ======================================================
``{ "type": "integer" } + options.format: "slider"`` An integer property with the ``slider`` format option.
==================================================== ======================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

=============== ======= ============================ ================================================================================================================================================================================================================================
Setting         Type    Default                      Description
=============== ======= ============================ ================================================================================================================================================================================================================================
``min``         Number  ``schema minimum, else 0``   Lower bound of the slider.
``max``         Number  ``schema maximum, else 100`` Upper bound of the slider.
``step``        Number  ``1``                        Step between two values.
``labelAlways`` Boolean ``false``                    Always display the value above the cursor.
Other           any                                  Every option is passed as a prop to `QSlider <https://quasar.dev/vue-components/slider#qslider-api>`__: ``min``, ``max``, ``step``, ``label``, ``labelAlways``, ``markers``, ``markerLabels``, ``snap``, ``color``, ``dense``...
=============== ======= ============================ ================================================================================================================================================================================================================================

Data
----

A number.

.. code:: json

   { "satisfaction": 7 }

See also the `Slider <https://www.obiba.org/quasar-json-form/#/controls/slider>`__ page of the Quasar JSON Form documentation, with live examples.
