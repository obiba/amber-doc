.. _computed:

Computed
========

A computed field has no rendering, nor condition or validation. The value is computed from a script, that will usually aggregate values captured by other fields.

Preview
-------

No preview.

Design
------

Definition
~~~~~~~~~~

.. include:: common-definition.rst

Settings
~~~~~~~~

.. list-table::
   :widths: 10 90
   :header-rows: 1

   * - Property
     - Definition
   * - ``Compute``
     - | The computation script, which is always evaluated.
       | There is no ``Condition`` script: instead of that, just return ``null`` when the computation data is not relevant.
       | Identically, any ``Default`` value can be returned by this computation script.
