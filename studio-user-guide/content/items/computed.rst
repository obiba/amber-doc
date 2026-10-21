.. _item_computed:

Computed
========

A control with ``format: "computed"`` writes the result of its ``compute`` rule into the data.

The `rule <https://www.obiba.org/quasar-json-form/#/start/rules>`__ expression is re-evaluated whenever the form data changes. The title and description are rendered as markdown above the value, the hint under it, and ``options.show: true`` displays the value; ``options.hidden: true`` displays nothing at all, the value being still computed and stored. A hidden computed control (by a ``visible`` rule) stores ``undefined``.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

============ ============================================ =================================================
Entry        Schema                                       UI schema
============ ============================================ =================================================
**Computed** ``{"type": "string", "format": "computed"}`` ``{"type": "Control", "rules": {"compute": ""}}``
============ ============================================ =================================================

Schema
------

The schema shapes that select this renderer:

========================================================== ========================================================================================
Schema                                                     Description
========================================================== ========================================================================================
``format: "computed" (schema or options) + rules.compute`` A value computed from the other fields with the ``compute`` rule, written into the data.
========================================================== ========================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

========== ======= ========= ============================================================================================
Setting    Type    Default   Description
========== ======= ========= ============================================================================================
``show``   Boolean ``false`` Display the computed value under the title (the ``noValue`` i18n key when undefined).
``hidden`` Boolean ``false`` Display nothing, not even the title and description: the value is still computed and stored.
========== ======= ========= ============================================================================================

Data
----

The result of the ``compute`` rule (``rules.compute`` on the schema property or the control), re-evaluated whenever the form data changes; ``undefined`` while the control is hidden.

.. code:: json

   { "quantity": 3, "price": 9.99, "total": 29.97 }

See also the `Computed <https://www.obiba.org/quasar-json-form/#/controls/computed>`__ page of the Quasar JSON Form documentation, with live examples.
