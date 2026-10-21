.. _cb_fe_format_text:

How to format text entries?
===========================

Open text fields are convenient for capturing data that are not known in advance (e.g. a phone number, an institutional ID etc.). In order to avoid writing complex validation rules, a mask can be defined to format the data when they are entered.

Step 1 - Add a Text control
---------------------------

From the *Controls* menu of the form builder, add a **Text** control (see :ref:`item_text`) and give it a key.

Note that it is not recommended to use a text field with a mask to capture date or time values. Use the **Date**, **Date and time** or **Time** controls instead.

Step 2 - Set the mask
---------------------

In the *Settings* section of the control properties, enter the **mask**. A mask is made of tokens, designating what type of character is expected at each position:

====== ==================================================
Token  Description
====== ==================================================
``#``  Numeric
``S``  Letter, a to z, case insensitive
``N``  Alphanumeric, case insensitive for letters
``A``  Letter, transformed to uppercase
``a``  Letter, transformed to lowercase
``X``  Alphanumeric, transformed to uppercase for letters
``x``  Alphanumeric, transformed to lowercase for letters
====== ==================================================

The text is stored as displayed, with the mask characters.

**Examples**

The phone number ``(514) 286-0768`` can be captured by the mask ``(###) ###-####``.

The institutional ID ``CA32 4455 6E5Z`` can be captured by the mask ``AA## #### XXXX``.

Step 3 - Check that the text is complete
----------------------------------------

The mask does not prevent an incomplete entry. In the *Validation* section, set the ``minLength`` of the text (14 for the phone number above), or a ``pattern`` (a regular expression) that the text must match, for instance ``^\(\d{3}\) \d{3}-\d{4}$``.
