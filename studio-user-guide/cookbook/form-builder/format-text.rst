How to format text entries?
===========================

Open text fields are convenient for capturing data that are not known in advance (e.g. a phone number, an institutional ID etc.). In order to avoid writing complex validation rules, a mask can be defined to format the data when they are entered.

Step 1 - Select Short Answer field
----------------------------------

Select the **Short answer** field type: the **Mask** setting will match the format of the data to capture. The mask can also be combined with a validation rule (to verify that all characters have been entered for instance).

Note that it is not recommended to use this open text field with a mask to capture date or time values. Use the **Date**, **Date and time** or **Time** specific field types instead.

Step - 2 Set the Mask
---------------------

A mask is made of tokens, designating what type of character is expected at each position. The possible mask tokens are:

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

**Examples**

The phone number ``(514) 286-0768`` can be captured by the mask ``(###) ###-####``.

The institutional ID ``CA32 4455 6E5Z`` can be captured by the mask ``AA## #### XXXX``.
