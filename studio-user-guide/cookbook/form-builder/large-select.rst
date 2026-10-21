.. _cb_fe_large_select:

How to make a select with a lot of options?
===========================================

When there are a lot of possible options it can be tricky to design a user friendly selection field.

Step 1 - Add a Typeahead control
--------------------------------

There are several controls for selecting among a list of options:

* **Radio buttons** and **Checkboxes**, where all the options are visible,
* **Select** and **Multiple select**, a dropdown menu,
* **Typeahead** and **Multiple typeahead**, an input with filtered suggestions.

The **Typeahead** (see :ref:`item_typeahead`) is the most appropriate: the options are proposed as the user types, so that there is no long list to scroll. The suggestions can also be extended with any text typed (the ``editable`` setting).

Step 2 - Set the options
------------------------

The options are the ``values`` of the control: a list of texts, or of ``{ "value": ..., "label": ... }`` objects when the stored value differs from the displayed label. A long list is more easily pasted in the *JSON* section of the control properties (the UI schema element), or in the *Source* panel of the form builder:

.. code-block:: json

  {
    "type": "Control",
    "scope": "#/properties/hospital",
    "options": {
      "format": "typeahead",
      "values": [
        { "value": "H2C", "label": "Ahuntsic Central" },
        { "value": "H2M", "label": "Ahuntsic East" },
        { "value": "H2B", "label": "Ahuntsic North" }
      ]
    }
  }

The labels can be translation keys: their translations are then added in the *Translations* panel, or uploaded as a CSV file (see :ref:`cb_fe_translation`).

When the stored values must be validated, use a **Select** with ``oneOf`` choices instead: the values that are not among the choices are then reported as errors.
