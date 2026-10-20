.. _item_radio_matrix:

Radio Matrix
============

An object with ``format: "radioGroupCollection"`` (or ``"radio-matrix"``) renders items as rows and values as radio columns.

Rows come from ``items`` (``[{ key, name }]``) and columns from ``values`` (``[{ key, caption }]`` or ``{ key: caption }``), in the control options or directly on the schema property as in the angular-schema-form add-on. Labels are translated and rendered as inline markdown. The data is ``{ [item.key]: value.key }``; a required matrix must have every row answered. Set ``options.dense: true`` for a compact table.

Schema definition and checkbox mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``options.checkboxMode: true`` renders one checkbox per item and stores ``{ [item.key]: boolean }``; a required matrix then needs at least one checked item.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================ ================================================ =====================================================================================================================================================
Entry            Schema                                           UI schema
================ ================================================ =====================================================================================================================================================
**Radio matrix** ``{"type": "object", "format": "radio-matrix"}`` ``{"type": "Control", "options": {"items": [{"key": "a", "label": "A"}], "values": [{"key": "yes", "label": "Yes"}, {"key": "no", "label": "No"}]}}``
================ ================================================ =====================================================================================================================================================

Schema
------

The schema shapes that select this renderer:

============================================================================ ======================================================
Schema                                                                       Description
============================================================================ ======================================================
``{ "type": "object", "format": "radioGroupCollection" \| "radio-matrix" }`` A table: one row per item, one radio column per value.
============================================================================ ======================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

================ =============== ========= ============================================================================================================================================================================================================================
Setting          Type            Default   Description
================ =============== ========= ============================================================================================================================================================================================================================
``items``        Array                     The rows, ``[{ key, name }]`` (``title``, ``label`` or ``caption`` are accepted for the label, which is rendered as inline markdown). Also read from ``items`` on the schema property, as in the angular-schema-form add-on.
``values``       Array \| Object           The columns, ``[{ key, caption }]`` or ``{ key: caption }``. Also read from ``values`` on the schema property.
``checkboxMode`` Boolean         ``false`` One checkbox per item instead of radio columns; the data is ``{ [item.key]: boolean }``.
``dense``        Boolean         ``false`` Dense table rows.
================ =============== ========= ============================================================================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

==================== ================================ =====================================================================================================================================================
Check                Message key                      Description
==================== ================================ =====================================================================================================================================================
``allItemsSelected`` ``radioMatrix.allItemsSelected`` A required matrix must have every row answered (at least one checked in checkbox mode), once the data exists; ``validationMessage.allItemsSelected``.
==================== ================================ =====================================================================================================================================================

Data
----

An object keyed by item key: the selected value key, or a boolean in checkbox mode. Read-only, a check mark shows the selection.

.. code:: json

   { "access": { "access_data": "yes", "access_bio_samples": "no" } }

See also the `Radio Matrix <https://www.obiba.org/quasar-json-form/#/controls/radio-matrix>`__ page of the Quasar JSON Form documentation, with live examples.
