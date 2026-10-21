.. _item_range:

Range
=====

An object with ``format: "range"`` renders a `QRange <https://quasar.dev/vue-components/range>`__ selecting two ends.

The value is the QRange model, an object ``{ min, max }`` of two numbers, and the schema declares the ``min`` and ``max`` properties so that ``minimum``, ``maximum`` or ``required`` apply. The format is read from the schema or from ``options.format``. The schema ``title`` and ``description`` are displayed above the range and the ``hint`` of the control element under it, unless there is an error. Every other option is passed to ``QRange``: ``min``, ``max``, ``step``, ``minRange``, ``maxRange``, ``dragRange``, ``markers``, ``label``, ``labelAlways``, ``color``... For a single value, see the `slider <https://www.obiba.org/quasar-json-form/#/controls/slider>`__.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========= =============================================================================================================== ==========================================================
Entry     Schema                                                                                                          UI schema
========= =============================================================================================================== ==========================================================
**Range** ``{"type": "object", "format": "range", "properties": {"min": {"type": "number"}, "max": {"type": "number"}}}`` ``{"type": "Control", "options": {"min": 0, "max": 100}}``
========= =============================================================================================================== ==========================================================

Schema
------

The schema shapes that select this renderer:

========================================== =====================================================================================
Schema                                     Description
========================================== =====================================================================================
``{ "type": "object" } + format: "range"`` An object property with the ``range`` format, in the schema or in ``options.format``.
========================================== =====================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======= ==== ======= ===========================================================================================================================================================================================================================================================================================
Setting Type Default Description
======= ==== ======= ===========================================================================================================================================================================================================================================================================================
Other   any          Every option is passed as a prop to `QRange <https://quasar.dev/vue-components/range#qrange-api>`__: ``min``, ``max``, ``step``, ``minRange``, ``maxRange``, ``dragRange``, ``dragOnlyRange``, ``label``, ``labelAlways``, ``markers``, ``markerLabels``, ``snap``, ``color``, ``dense``...
======= ==== ======= ===========================================================================================================================================================================================================================================================================================

Data
----

An object ``{ min, max }`` of two numbers (the QRange model), ``undefined`` when neither end is set. The ``min`` and ``max`` sub-properties are validated by AJV like any number.

.. code:: json

   { "ages": { "min": 20, "max": 60 } }

See also the `Range <https://www.obiba.org/quasar-json-form/#/controls/range>`__ page of the Quasar JSON Form documentation, with live examples.
