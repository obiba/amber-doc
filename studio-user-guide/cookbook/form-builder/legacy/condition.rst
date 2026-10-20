.. _cb_condition:

How to make fields conditional?
===============================

A conditional field is a field that depends of data collected by one or more fields. The condition is logical value:

* ``true``, the field is visible and data can be captured,
* ``false``, the field is not visible and has no value (i.e. value will be removed when switching from ``true`` to ``false`` condition).

The condition is a short Javascript code. In the context of the execution of this code, the other field values can be accessed with the following syntax:

.. code::

  $('VARIABLE')

where ``VARIABLE`` is the name of the field from which the value is to retrieved. When the field is in a group, use a ``.`` for building the full name of the field. For instance, if the field with name ``VARIABLE`` is in a group with name ``GROUP``, the value of the field will be:

.. code::

  $('GROUP.VARIABLE')

**Examples**

If the field is a numeric value:

.. code::

  $('VARIABLE') > 12

If the field is an array value (case of multiple choices), to check that there is a value and that 2 choices have been made exactly:

.. code::

  $('VARIABLE') && $('VARIABLE').length === 2

If the field is a string value representing a date, to check that there is a value and that the date is not in the future:

.. code::

  $('VARIABLE') && Date.parse($('VARIABLE')) <= Date.now()
