.. _item_date:

Date
====

A string with ``format: "date"``, ``"datepicker"``, ``"year-month"`` or ``"ymdatepicker"`` renders an input with a `QDate <https://quasar.dev/vue-components/date>`__ popup.

``format: "date"`` stores an ISO date (``YYYY-MM-DD``) validated by AJV. ``year-month`` stores ``YYYY-MM`` with a month picker.

Mask and bounds
~~~~~~~~~~~~~~~

``datepicker`` controls store the date in the ``dateFormat`` mask (``YYYY-MM-DD`` by default; angular-strap masks such as ``dd/MM/yyyy`` are accepted). ``min`` and ``max``, as options or as `rules <https://www.obiba.org/quasar-json-form/#/start/rules>`__ naming another field, bound the value and the picker; the messages can be customized with ``validationMessage.dateMin`` / ``dateMax`` / ``dateRange`` / ``dateInvalid``. The options can also be nested under ``dateOptions``, as in angular-schema-form.

Year and month references
~~~~~~~~~~~~~~~~~~~~~~~~~

``ymdatepicker`` ties the date to a year field and a month field (``yearRef`` / ``monthRef``, siblings of the control or root fields). The input is disabled until both are set, the value defaults to the first day of that month (``lastDay: true`` for the last one) and follows them.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================== ============================================== =======================
Entry              Schema                                         UI schema
================== ============================================== =======================
**Date**           ``{"type": "string", "format": "date"}``       ``{"type": "Control"}``
**Year and month** ``{"type": "string", "format": "year-month"}`` ``{"type": "Control"}``
================== ============================================== =======================

Schema
------

The schema shapes that select this renderer:

============================================== ============================================================================
Schema                                         Description
============================================== ============================================================================
``{ "type": "string", "format": "date" }``     ISO date (``YYYY-MM-DD``), validated by AJV; the mask option does not apply.
``format: "datepicker" (schema or options)``   Date in the ``dateFormat`` mask (``YYYY-MM-DD`` by default).
``format: "year-month" (schema or options)``   Month picker, ``YYYY-MM`` by default.
``format: "ymdatepicker" (schema or options)`` Day within the month given by the ``yearRef`` and ``monthRef`` fields.
============================================== ============================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

=============== ======================== ============== ================================================================================================================================================================
Setting         Type                     Default        Description
=============== ======================== ============== ================================================================================================================================================================
``dateFormat``  String                   ``YYYY-MM-DD`` Mask of the stored value (Quasar masks; angular-strap masks such as ``yyyy-MM-dd`` or ``dd/MM/yyyy`` are accepted). ``YYYY-MM`` for ``year-month``.
``min``         String \| Number \| Date                Lower bound, in the mask format or ISO; the ``min`` rule of the control works too.
``max``         String \| Number \| Date                Upper bound, in the mask format or ISO; the ``max`` rule of the control works too.
``yearRef``     String                                  ``ymdatepicker``: name of the year field (a sibling of the control, else a root field) the date must belong to.
``monthRef``    String                                  ``ymdatepicker``: name of the month field (1 to 12).
``lastDay``     Boolean                  ``false``      ``ymdatepicker``: default to the last day of the referenced month instead of the first one.
``dateOptions`` Object                                  The same options nested, as in angular-schema-form: ``{ dateFormat, min, max, yearRef, monthRef, lastDay, validationMessage }``. Direct options take precedence.
Other           any                                     Every other option is passed as a prop to `QInput <https://quasar.dev/vue-components/input#qinput-api>`__.
=============== ======================== ============== ================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

================= ===================== ====================================================================================
Check             Message key           Description
================= ===================== ====================================================================================
``dateInvalid``   ``error.dateInvalid`` The value does not match the mask (``{format}``); ``validationMessage.dateInvalid``.
``dateRange``     ``error.dateRange``   Outside ``min`` and ``max`` (``{min}``, ``{max}``); ``validationMessage.dateRange``.
``dateMin``       ``error.dateMin``     Before ``min`` (``{limit}``); ``validationMessage.dateMin``.
``dateMax``       ``error.dateMax``     After ``max`` (``{limit}``); ``validationMessage.dateMax``.
``invalidYMDate`` ``error.dateRange``   ``ymdatepicker``: not in the referenced month; ``validationMessage.invalidYMDate``.
================= ===================== ====================================================================================

Data
----

A string in the mask format. The errors are reported with the ``date`` keyword. The picker only offers the dates within the bounds; the input is disabled until the ``yearRef`` / ``monthRef`` fields are set.

.. code:: json

   { "birthDate": "1990-05-17", "period": "2024-03" }

See also the `Date <https://www.obiba.org/quasar-json-form/#/controls/date>`__ page of the Quasar JSON Form documentation, with live examples.
