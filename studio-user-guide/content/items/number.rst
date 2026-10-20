.. _item_number:

Number
======

A ``{ "type": "number" }`` or ``{ "type": "integer" }`` property renders a numeric `QInput <https://quasar.dev/vue-components/input>`__.

The value is stored as a JavaScript number; an emptied input stores ``undefined`` so that ``required`` applies. ``minimum``, ``maximum``, ``exclusiveMinimum``, ``exclusiveMaximum``, ``multipleOf`` and the ``integer`` type are validated by AJV. An integer with ``options.format`` ``slider`` or ``rating`` renders a `slider <https://www.obiba.org/quasar-json-form/#/controls/slider>`__ or a `rating <https://www.obiba.org/quasar-json-form/#/controls/rating>`__ instead.

Quasar props
~~~~~~~~~~~~

Every option is passed to ``QInput``; the native ``step``, ``min`` and ``max`` attributes drive the spinner of the browser.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

=========== ======================= =======================
Entry       Schema                  UI schema
=========== ======================= =======================
**Number**  ``{"type": "number"}``  ``{"type": "Control"}``
**Integer** ``{"type": "integer"}`` ``{"type": "Control"}``
=========== ======================= =======================

Schema
------

The schema shapes that select this renderer:

========================= =========================================================================
Schema                    Description
========================= =========================================================================
``{ "type": "number" }``  Any number property.
``{ "type": "integer" }`` Any integer property without ``options.format`` ``slider`` or ``rating``.
========================= =========================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======= ==== ======= ===========================================================================================================================================================================================================================================================
Setting Type Default Description
======= ==== ======= ===========================================================================================================================================================================================================================================================
Other   any          Every option is passed as a prop or attribute to `QInput <https://quasar.dev/vue-components/input#qinput-api>`__ (``type`` is forced to ``number``): ``outlined``, ``dense``, ``prefix``, ``suffix``, and the native ``step``, ``min``, ``max`` attributes.
======= ==== ======= ===========================================================================================================================================================================================================================================================

Data
----

A JavaScript number (``Number(value)`` of the input). An emptied input stores ``undefined``, so that ``required`` applies. The schema keywords ``minimum``, ``maximum``, ``exclusiveMinimum``, ``exclusiveMaximum`` and ``multipleOf`` are validated by AJV, as well as ``type: integer``.

.. code:: json

   { "age": 42, "price": 9.99 }

See also the `Number <https://www.obiba.org/quasar-json-form/#/controls/number>`__ page of the Quasar JSON Form documentation, with live examples.
