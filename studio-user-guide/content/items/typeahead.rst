.. _item_typeahead:

Typeahead
=========

A string with ``format: "typeahead"`` is an input with filtered suggestions.

The suggestions come from ``options.values`` (strings or ``{ label, value }``), or the schema ``examples`` / ``enum``. By default the value must be one of the suggestions; ``options.editable: true`` accepts any text typed, added with Enter.

On an array property (``{ "type": "array", "items": { "type": "string" }, "format": "typeahead" }``), several values are selected and displayed as chips; the data is the array of the values, ``undefined`` when there is none.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

====================== ============================================================================================== ==========================================================
Entry                  Schema                                                                                         UI schema
====================== ============================================================================================== ==========================================================
**Typeahead**          ``{"type": "string", "format": "typeahead"}``                                                  ``{"type": "Control", "options": {"values": ["A", "B"]}}``
**Multiple typeahead** ``{"type": "array", "format": "typeahead", "uniqueItems": true, "items": {"type": "string"}}`` ``{"type": "Control", "options": {"values": ["A", "B"]}}``
====================== ============================================================================================== ==========================================================

Schema
------

The schema shapes that select this renderer:

================================================================================================ =====================================
Schema                                                                                           Description
================================================================================================ =====================================
``{ "type": "string" } + format: "typeahead" (schema or options)``                               Text input with filtered suggestions.
``{ "type": "array", "items": { "type": "string" } } + format: "typeahead" (schema or options)`` Several values, displayed as chips.
================================================================================================ =====================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============ ======= ========= ==================================================================================================================================================================================================================
Setting      Type    Default   Description
============ ======= ========= ==================================================================================================================================================================================================================
``values``   Array             The suggestions: strings, or ``{ label, value }`` objects (``name`` / ``title`` and ``key`` / ``const`` are accepted too). Defaults to the schema ``examples``, then ``enum``. Labels are translated with ``t()``.
``editable`` Boolean ``false`` Accept any typed text (added with Enter) instead of only the suggestions.
Other        any               Every other option is passed as a prop to `QSelect <https://quasar.dev/vue-components/select#qselect-api>`__: ``outlined``, ``dense``, ``hideDropdownIcon``...
============ ======= ========= ==================================================================================================================================================================================================================

Data
----

The selected (or typed, when ``editable``) string, or the array of strings on an array property; a cleared input stores ``undefined``.

.. code:: json

   { "role": "Data manager" }

See also the `Typeahead <https://www.obiba.org/quasar-json-form/#/controls/typeahead>`__ page of the Quasar JSON Form documentation, with live examples.
