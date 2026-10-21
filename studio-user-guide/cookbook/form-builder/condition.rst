.. _cb_fe_condition:

How to make fields conditional?
===============================

A conditional field is a field that depends of data collected by one or more fields. In the *Rules* section of the element properties, the **Visible when** expression is evaluated with the form data each time it changes:

* ``true``, the element is visible and data can be captured,
* ``false``, the element is not visible and has no value (i.e. the value is cleared when the expression switches from ``true`` to ``false``).

The expression can also be set on a layout (a group, a section, a tab...): it then applies to all its elements. **Enabled when** works the same way, the element being displayed but disabled. **Required when** makes a field mandatory depending on other data.

The other fields are named by their key; a field inside a group is named by the key of the group and the key of the field, separated by a ``.``: for instance ``GROUP.VARIABLE``. The expressions are described in :ref:`form_engine_expressions`.

**Examples**

If the field is a numeric value:

.. code::

  VARIABLE > 12

If the field is a selection value:

.. code::

  VARIABLE == 'other'

If the field is an array value (case of multiple choices), to check that 2 choices have been made exactly, or that a given choice is selected:

.. code::

  length(VARIABLE) == 2
  contains(VARIABLE, 'fever')

If the field is a date, to check that there is a value and that the date is not in the future:

.. code::

  isNotEmpty(VARIABLE) && VARIABLE <= today()

The options of a select or of radio buttons can be conditional too: in the *JSON* section, add ``"rules": { "visible": "..." }`` to the ``oneOf`` entry of the option (see :ref:`item_select`).
