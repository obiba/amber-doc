How to make a computed field?
=============================

A computed field is a field that do not require the user to enter a value, it is computed with other fields values.

The computation rule is a short Javascript code. Other field values can be accessed with the following syntax:

.. code::

  $('VARIABLE')

where ``VARIABLE`` is the name of the field from which the value is to retrieved. When the field is in a group, use a ``.`` for building the full name of the field. For instance, if the field with name ``VARIABLE`` is in a group with name ``GROUP``, the value of the field will be:

.. code::

  $('GROUP.VARIABLE')

**Examples**

The computed value is the sum of other numeric values:

.. code::

  $('VAR1') + $('VAR2')
