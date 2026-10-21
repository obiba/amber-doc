.. _item_radio_checkbox:

Radio Buttons and Checkboxes
============================

The ``radio``, ``checkbox`` and ``toggle`` format options render the values of a `selection <https://www.obiba.org/quasar-json-form/#/controls/select>`__ as a `QOptionGroup <https://quasar.dev/vue-components/option-group>`__.

``options.format: "radio"`` on a single selection (``enum`` or ``oneOf``) renders radio buttons.

Checkboxes and toggles
~~~~~~~~~~~~~~~~~~~~~~

On a multiple selection (array with ``uniqueItems``), ``options.format: "checkbox"`` or ``"toggle"`` renders one checkbox or toggle per value. The data is always an array, empty when nothing is checked.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================= ============================================================================================================================================== ==========================================================
Entry             Schema                                                                                                                                         UI schema
================= ============================================================================================================================================== ==========================================================
**Radio buttons** ``{"type": "string", "oneOf": [{"const": "a", "title": "A"}, {"const": "b", "title": "B"}]}``                                                  ``{"type": "Control", "options": {"format": "radio"}}``
**Checkboxes**    ``{"type": "array", "uniqueItems": true, "items": {"type": "string", "oneOf": [{"const": "a", "title": "A"}, {"const": "b", "title": "B"}]}}`` ``{"type": "Control", "options": {"format": "checkbox"}}``
================= ============================================================================================================================================== ==========================================================

Schema
------

The schema shapes that select this renderer:

===================================================================================================================== ================================================================================
Schema                                                                                                                Description
===================================================================================================================== ================================================================================
``{ "type": "string", "enum": [...] } + options.format: "radio"``                                                     Radio buttons, one per ``enum`` value.
``{ "oneOf": [{ "const", "title" }] } + options.format: "radio"``                                                     Radio buttons, one per ``oneOf`` entry (``rules.visible`` on an entry hides it).
``{ "type": "array", "uniqueItems": true, "items": { "enum" \| "oneOf" } } + options.format: "checkbox" \| "toggle"`` One checkbox (or toggle) per value, the data is an array.
===================================================================================================================== ================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

========== ====== ======= ==========================================================================================================================================================================================
Setting    Type   Default Description
========== ====== ======= ==========================================================================================================================================================================================
``format`` String         ``radio`` for a single selection; ``checkbox`` or ``toggle`` for a multiple selection.
Other      any            Every other option is passed as a prop to `QOptionGroup <https://quasar.dev/vue-components/option-group#qoptiongroup-api>`__: ``inline``, ``color``, ``dense``, ``leftLabel``, ``size``...
========== ====== ======= ==========================================================================================================================================================================================

Data
----

The selected value, or an array of values for checkboxes and toggles (an empty array when nothing is checked). Read-only, the selection is displayed but ignores clicks.

.. code:: json

   { "size": "M", "toppings": ["cheese", "olives"] }

See also the `Radio Buttons and Checkboxes <https://www.obiba.org/quasar-json-form/#/controls/options>`__ page of the Quasar JSON Form documentation, with live examples.
