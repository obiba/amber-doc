.. _cb_fe_computed_field:

How to make a computed field?
=============================

A computed field is a field that does not require the user to enter a value: it is computed with the values of other fields, and stored with the collected data.

Step 1 - Add a Computed control
-------------------------------

From the *Controls* menu of the form builder, add a **Computed** control (see :ref:`item_computed`). By default the computed value is not displayed; the ``show`` setting displays it, under the title.

Step 2 - Set the computed value
-------------------------------

In the *Rules* section, the **Computed value** is an expression that is evaluated each time the form data change (see :ref:`form_engine_expressions`). The other fields are named by their key; a field inside a group is named ``GROUP.VARIABLE``.

**Examples**

The computed value is the sum of other numeric values:

.. code::

  VAR1 + VAR2

The body mass index, when both the weight (kg) and the height (m) are entered:

.. code::

  isNumber(WEIGHT) && isNumber(HEIGHT) ? WEIGHT / (HEIGHT * HEIGHT) : undefined

Note that only the functions listed in :ref:`form_engine_expressions` can be called: the JavaScript methods, such as ``toFixed()``, are not available.

The age group, recoded from the age with thresholds:

.. code::

  map(AGE, [18, 'minor', 65, 'adult', 65, 'senior'])

The computed value can be used in the other expressions, and in the texts of the form with a placeholder: ``Your BMI is {{ BMI }}``.
