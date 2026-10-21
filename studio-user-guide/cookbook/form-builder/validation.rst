.. _cb_fe_validation:

How to validate field values?
=============================

A field can be validated in three ways, from the simplest to the most flexible.

Step 1 - Use the schema constraints
-----------------------------------

The *Validation* section of the control properties proposes the constraints that apply to the type of the field:

* text: ``minLength``, ``maxLength``, ``pattern`` (a regular expression), ``format``,
* number: ``minimum``, ``maximum``, ``exclusiveMinimum``, ``exclusiveMaximum``, ``multipleOf``,
* list or multiple selection: ``minItems``, ``maxItems``, ``uniqueItems``.

Some controls have their own checks, set in the *Settings* section: the word limits of a text, the minimum and maximum of a date, the number of files etc.

Step 2 - Add validation rules
-----------------------------

For a check involving the value of other fields, add a **validation rule** in the *Validation* section: an expression that must be true, and the message displayed when it is false. The value of the field is named by its key, as the other fields (see :ref:`form_engine_expressions`). A field can have several validation rules, each with its own message.

As an empty value does not satisfy most of the expressions, the validation rule of an optional field should also accept the empty value.

**Examples**

The text entered must have at least 10 words:

.. code::

  isEmpty(COMMENT) || wordCount(COMMENT) >= 10

The number entered must be lower than another field value:

.. code::

  isEmpty(CIGARETTES) || CIGARETTES < CIGARETTES_MAX

The date can be empty or not be in the future:

.. code::

  isEmpty(VISIT_DATE) || VISIT_DATE <= today()

The arrival date and time at the hospital (a **Date and time** field, stored as ``YYYY-MM-DD HH:mm``) must be after the trauma date and time, and not in the future:

.. code::

  isEmpty(ARRIVAL.DATETIME) || (parseDate(ARRIVAL.DATETIME) <= now() && parseDate(ARRIVAL.DATETIME) >= parseDate(TRAUMA.DATETIME))

Step 3 - Customize the error messages
-------------------------------------

The messages of the schema constraints are built-in, in English and French. A form can carry its own messages in its translations, for a field (``<key>.error.<constraint>``, for instance ``AGE.error.minimum``) or for the whole form (``error.<constraint>``, for instance ``error.required``). See :ref:`form_engine_validation`.
