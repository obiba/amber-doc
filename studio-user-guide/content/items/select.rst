.. _item_select:

Select
======

A property with ``enum`` or ``oneOf`` values renders a `QSelect <https://quasar.dev/vue-components/select>`__.

With ``enum``, each value is its own label (translated with vue-i18n when it is a key). With ``oneOf``, each entry is ``{ const, title }``: the ``const`` is stored and the ``title`` displayed, which also allows non-string values.

Multiple selection
~~~~~~~~~~~~~~~~~~

An array with ``uniqueItems: true`` whose ``items`` have ``enum`` or ``oneOf`` values is a multiple selection. ``minItems`` and ``maxItems`` are validated by AJV. Add ``options.format: "checkbox"`` to render `checkboxes <https://www.obiba.org/quasar-json-form/#/controls/options>`__ instead.

Dynamic options
~~~~~~~~~~~~~~~

A ``oneOf`` entry accepts its own ``rules.visible`` `rule <https://www.obiba.org/quasar-json-form/#/start/rules>`__: the option is listed only when the rule is true, and a selected value that becomes hidden is cleared. This is how dependent selects are expressed within the schema.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

=================== ============================================================================================================================================== =======================
Entry               Schema                                                                                                                                         UI schema
=================== ============================================================================================================================================== =======================
**Select**          ``{"type": "string", "oneOf": [{"const": "a", "title": "A"}, {"const": "b", "title": "B"}]}``                                                  ``{"type": "Control"}``
**Multiple select** ``{"type": "array", "uniqueItems": true, "items": {"type": "string", "oneOf": [{"const": "a", "title": "A"}, {"const": "b", "title": "B"}]}}`` ``{"type": "Control"}``
=================== ============================================================================================================================================== =======================

Schema
------

The schema shapes that select this renderer:

============================================================================ ============================================================================================================================================================
Schema                                                                       Description
============================================================================ ============================================================================================================================================================
``{ "type": "string", "enum": [...] }``                                      Single selection among the ``enum`` values; each value is translated with ``t()`` for its label.
``{ "oneOf": [{ "const": ..., "title": ... }] }``                            Single selection among ``oneOf`` entries: ``const`` is the value, ``title`` the label. An entry with ``rules.visible`` is listed only when its rule is true.
``{ "type": "array", "uniqueItems": true, "items": { "enum" \| "oneOf" } }`` Multiple selection, the data is an array of values.
============================================================================ ============================================================================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======= ==== ======= =================================================================================================================================================================================================================================================================================================================================================
Setting Type Default Description
======= ==== ======= =================================================================================================================================================================================================================================================================================================================================================
Other   any          Every option is passed as a prop to `QSelect <https://quasar.dev/vue-components/select#qselect-api>`__: ``outlined``, ``dense``, ``useChips``, ``optionsDense``, ``behavior``, ``displayValue``... ``emitValue`` and ``mapOptions`` are always set, ``multiple`` follows the schema type and ``clearable`` is set unless the control is required.
======= ==== ======= =================================================================================================================================================================================================================================================================================================================================================

Data
----

The selected value (``enum`` value or ``oneOf`` ``const``), or an array of values for a multiple selection. A cleared selection stores ``undefined``. When the options change (a ``oneOf`` entry becomes hidden) a selection that is no longer listed is cleared.

.. code:: json

   { "role": "admin", "tags": ["a", "b"] }

See also the `Select <https://www.obiba.org/quasar-json-form/#/controls/select>`__ page of the Quasar JSON Form documentation, with live examples.
