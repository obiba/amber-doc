.. _item_toggle:

Toggle
======

A ``{ "type": "boolean" }`` property renders a `QToggle <https://quasar.dev/vue-components/toggle>`__.

The schema ``title`` and ``description`` are displayed above the toggle, ``label`` on the control element is the text of the toggle and ``hint`` is displayed under it.

A toggle that must be on
~~~~~~~~~~~~~~~~~~~~~~~~

Do not express a boolean that must be checked with ``const: true`` (nor ``enum: [true]``): the JSON Forms enum tester matches any schema with a ``const`` or ``enum`` keyword, whatever its type, and its select renderer outranks the toggle renderer. The property is then rendered as a `select <https://www.obiba.org/quasar-json-form/#/controls/select>`__ whose options are built from ``enum``, which is missing: an empty dropdown.

Wrap the constraint in ``allOf`` instead. The property stays a plain boolean for the renderers, so it gets a toggle, and AJV still reports a "must be equal to true" error on it while it is off. The toggle has no message area, so the error is only visible in the ``errors`` model of the form (see `validation <https://www.obiba.org/quasar-json-form/#/start/json-form>`__).

.. code:: json

   {
     "terms": { "type": "boolean", "title": "I accept the terms", "allOf": [{ "const": true }] }
   }

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========== ======================= =======================
Entry      Schema                  UI schema
========== ======================= =======================
**Toggle** ``{"type": "boolean"}`` ``{"type": "Control"}``
========== ======================= =======================

Schema
------

The schema shapes that select this renderer:

========================= =====================
Schema                    Description
========================= =====================
``{ "type": "boolean" }`` Any boolean property.
========================= =====================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======= ==== ======= ===========================================================================================================================================================================================================================
Setting Type Default Description
======= ==== ======= ===========================================================================================================================================================================================================================
Other   any          Every other option is passed as a prop to `QToggle <https://quasar.dev/vue-components/toggle#qtoggle-api>`__: ``color``, ``icon``, ``checkedIcon``, ``uncheckedIcon``, ``size``, ``leftLabel``, ``keepColor``, ``dense``...
======= ==== ======= ===========================================================================================================================================================================================================================

Data
----

``true`` or ``false``. Read-only, the toggle is displayed but ignores clicks.

.. code:: json

   { "subscribed": true }

See also the `Toggle <https://www.obiba.org/quasar-json-form/#/controls/toggle>`__ page of the Quasar JSON Form documentation, with live examples.
