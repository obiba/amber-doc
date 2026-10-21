.. _item_list:

List
====

An array of objects or of primitives renders a list with add, remove and reorder buttons.

By default an object item renders one control per property, and a primitive item is the control itself. A new item gets the default value of the item schema. Read-only, the buttons are hidden.

Item layout and options
~~~~~~~~~~~~~~~~~~~~~~~

``options.items`` is the UI schema of one item, with ``Control`` scopes relative to the item schema (``#`` for the item itself). ``minItems`` / ``maxItems`` from the schema (or the ``min`` / ``max`` rules) disable the remove and add buttons.

Primitives
~~~~~~~~~~

Arrays of strings, numbers, booleans, or of formatted objects such as localized strings, render the item itself. Enum arrays with ``uniqueItems`` render a `selection <https://www.obiba.org/quasar-json-form/#/controls/select>`__ instead.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

======== ==================================================================== =======================
Entry    Schema                                                               UI schema
======== ==================================================================== =======================
**List** ``{"type": "array", "items": {"type": "object", "properties": {}}}`` ``{"type": "Control"}``
======== ==================================================================== =======================

Schema
------

The schema shapes that select this renderer:

==================================================================================================== ===================================================================================================================================================================
Schema                                                                                               Description
==================================================================================================== ===================================================================================================================================================================
``{ "type": "array", "items": { "type": "object" } }``                                               A list of objects, one control per property of an item by default.
``{ "type": "array", "items": { "type": "string" \| "number" \| "boolean" \| { "format": ... } } }`` A list of primitives (or of formatted objects such as localized strings), the item itself is the control. Enum arrays with ``uniqueItems`` are a selection instead.
==================================================================================================== ===================================================================================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

================ ======= ========= =======================================================================================================================================================================================================================================
Setting          Type    Default   Description
================ ======= ========= =======================================================================================================================================================================================================================================
``items``        Object            UI schema of one item: ``Control`` scopes are relative to the item schema (``#/properties/x``, or ``#`` for the item itself). By default a ``VerticalLayout`` with one control per property, or the item control with ``label: false``.
``addLabel``     String            Label of the add button, translated with ``t()``; defaults to the ``add-item`` i18n key.
``addIcon``      String  ``add``   Icon of the add button.
``ordering``     Boolean ``true``  Show the move up / move down buttons.
``confirmation`` Boolean ``false`` Ask for confirmation before removing an item (``confirm-remove-item``, ``cancel`` and ``remove`` i18n keys).
Other            any               Every other option is passed as a prop to the `QList <https://quasar.dev/vue-components/list-and-list-items#qlist-api>`__: ``bordered``, ``separator``, ``dense``, ``padding``...
================ ======= ========= =======================================================================================================================================================================================================================================

Data
----

An array. A new item gets the default value of the item schema. ``minItems`` / ``maxItems`` from the schema (or the ``min`` / ``max`` rules) disable the remove / add buttons; AJV also validates them. Read-only, the buttons are hidden. A hidden list (``rules.visible``) is emptied.

.. code:: json

   { "comments": [{ "date": "2024-01-01", "message": "Hello" }], "tags": ["a", "b"] }

See also the `List <https://www.obiba.org/quasar-json-form/#/controls/list>`__ page of the Quasar JSON Form documentation, with live examples.
