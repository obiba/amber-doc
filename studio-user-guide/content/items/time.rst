.. _item_time:

Time
====

A string with ``format: "time"`` renders an input with a `QTime <https://quasar.dev/vue-components/time>`__ popup.

``time`` stores ``HH:mm``; ``fulltime`` stores ``HH:mm:ss`` and shows the seconds in the picker. AJV validates ``time`` as the picker stores it (seconds and timezone optional).

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

======== ======================================== =======================
Entry    Schema                                   UI schema
======== ======================================== =======================
**Time** ``{"type": "string", "format": "time"}`` ``{"type": "Control"}``
======== ======================================== =======================

Schema
------

The schema shapes that select this renderer:

========================================== ===================================================================================================================
Schema                                     Description
========================================== ===================================================================================================================
``{ "type": "string", "format": "time" }`` ``HH:mm`` input with a time picker (24h); validated by AJV as the picker stores it (seconds and timezone optional).
``format: "fulltime" (schema or options)`` ``HH:mm:ss``, the picker shows the seconds.
========================================== ===================================================================================================================

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

A string, ``HH:mm`` or ``HH:mm:ss``. Read-only, the picker icon is hidden.

.. code:: json

   { "start": "09:30", "precise": "09:30:15" }

See also the `Time <https://www.obiba.org/quasar-json-form/#/controls/time>`__ page of the Quasar JSON Form documentation, with live examples.
