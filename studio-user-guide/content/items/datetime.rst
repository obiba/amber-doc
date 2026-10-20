.. _item_datetime:

Date and Time
=============

A string with ``format: "date-time"`` renders an input with a date picker and a time picker.

``date-time`` stores ``YYYY-MM-DD HH:mm``; ``date-fulltime`` adds the seconds. AJV validates ``date-time`` as the pickers store it (a ``T`` separator, seconds and timezone are also accepted).

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================= ============================================= =======================
Entry             Schema                                        UI schema
================= ============================================= =======================
**Date and time** ``{"type": "string", "format": "date-time"}`` ``{"type": "Control"}``
================= ============================================= =======================

Schema
------

The schema shapes that select this renderer:

=============================================== ================================================================================================================================================================
Schema                                          Description
=============================================== ================================================================================================================================================================
``{ "type": "string", "format": "date-time" }`` ``YYYY-MM-DD HH:mm`` input with a date picker and a time picker; validated by AJV as the pickers store it (``T`` separator, seconds and timezone also accepted).
``format: "date-fulltime" (schema or options)`` ``YYYY-MM-DD HH:mm:ss``, with seconds.
=============================================== ================================================================================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======= ==== ======= ====================================================================================================
Setting Type Default Description
======= ==== ======= ====================================================================================================
Other   any          Every option is passed as a prop to `QInput <https://quasar.dev/vue-components/input#qinput-api>`__.
======= ==== ======= ====================================================================================================

Data
----

A string, ``YYYY-MM-DD HH:mm`` or ``YYYY-MM-DD HH:mm:ss``.

.. code:: json

   { "meeting": "2024-03-15 14:30" }

See also the `Date and Time <https://www.obiba.org/quasar-json-form/#/controls/datetime>`__ page of the Quasar JSON Form documentation, with live examples.
