The following dynamic properties apply:

.. list-table::
   :widths: 10 90
   :header-rows: 1

   * - Property
     - Definition
   * - ``Condition``
     - | The condition makes an item visible or not depending of other data. It is a small script which returns a logical value: ``true`` when item is visible.
       | When no condition is specified (which is the default), the item is visible.
       | See :ref:`cb_condition`
   * - ``Validation``
     - | The validation specifies whether the data entry is correct. It is a small script which returns a logical value: ``true`` when item value is valid.
       | Note that this validation script is not evaluated when the visibility ``Condition`` is not satisfied.
       | See :ref:`cb_validation`
   * - ``Validation error message``
     - The validation error message to be displayed when validation fails.
