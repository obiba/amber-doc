.. _cb_validation:

How to validate field values?
=============================

An open field needs to be validated.

The validation is a short Javascript code. In the context of the execution of this code, the ``val`` Javascript variable represents the value captured by the field to validate. The other field values can be accessed with the following syntax:

.. code::

  $('VARIABLE')

where ``VARIABLE`` is the name of the field from which the value is to retrieved. When the field is in a group, use a ``.`` for building the full name of the field. For instance, if the field with name ``VARIABLE`` is in a group with name ``GROUP``, the value of the field will be:

.. code::

  $('GROUP.VARIABLE')

**Validation message**

When field validation fails, a validation message should be prompted to help user to correct the answer.

**Examples**

The text entered must have at least 10 characters:

.. code::

  val && val.length >= 10

The number entered must be lower than another field value:

.. code::

  val && val < $('VARIABLE')

The date can be empty or not be in the future:

.. code::

  val === null || Date.parse(val) <= Date.now()

Working with date and time can be tricky, as the supported text format of the date can be different from one browser to another. For instance ``2022-03-07`` (ISO 8601 format, this is how a date value is captured) is not supported by Safari. For Safari ``2022/03/07`` is a valid date format, which works for the other browsers as well. Then we will use the ``replace()`` Javascript function to switch from one format to the other. The following validates that the arrival date at the hospital is either empty or is not in the future and is after the trauma date time:

.. code::

  val == null ||
    (Date.parse($('ARRIVAL.DATE').replace(/-/g, '/') + ' ' + val) <= Date.now()
      && Date.parse($('ARRIVAL.DATE').replace(/-/g, '/') + ' ' + val) >= Date.parse($('TRAUMA.DATE').replace(/-/g, '/') + ' ' + $('TRAUMA.TIME')))
