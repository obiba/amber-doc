.. _form_items:

Form Items
==========

The items of a form are the elements of its UI schema: the **controls**, which capture the data of a property of the schema, and the **layouts**, which arrange the controls (groups, sections, tabs...). They are added to the form from the palette of the :ref:`form builder <form_engine>`, which has a *Controls* and a *Layouts* menu.

The forms designed with the previous form engine are made of the :ref:`legacy form items <legacy_form_items>`.

Element properties
------------------

When an element is selected in the outline of the form builder, its properties are displayed in the following sections:

.. list-table::
   :widths: 20 80
   :header-rows: 1

   * - Section
     - Description
   * - Key
     - The name of the property of a control, i.e. the variable name associated to the collected data, and used in the rules. A key starts with a letter and has letters, digits and underscores only. Renaming a key lists the rules that still mention the previous name.
   * - Required
     - Whether a value is mandatory. Note that a hidden or disabled control is not validated.
   * - Texts
     - The texts of the element (title, description, label, hint, text of a label...) in the current language of the builder. Switch the language at the top of the builder to edit the other translations.
   * - Choices
     - The values a selection accepts: the value stored in the data, and the label displayed in the current language.
   * - Settings
     - The settings of the renderer of the element (see :ref:`item_common_settings` and the page of each control). An empty field uses the default of the renderer.
   * - Validation
     - | The schema constraints on the value of a control, and the default value of a new record:
       | text: ``default``, ``minLength``, ``maxLength``, ``pattern``, ``format``;
       | number: ``default``, ``minimum``, ``maximum``, ``exclusiveMinimum``, ``exclusiveMaximum``, ``multipleOf``;
       | list or multiple selection: ``minItems``, ``maxItems``, ``uniqueItems``;
       | toggle: ``default``.
       | Then the validation rules: expressions that must be true, each with its error message (see :ref:`form_engine_rules`).
   * - Rules
     - *Visible when*, *Enabled when* and *Required when* expressions, and the *Computed value* of a computed control (see :ref:`form_engine_rules`).
   * - JSON
     - The UI schema element and the property schema, for the settings that have no dedicated field.

Common texts
------------

The texts of every control, in the *Texts* section of the element properties, or keys of the UI schema element:

==================== =============== =======================================================================================================================================================================================================================================================================================================================================================================
Key                  Type            Description
==================== =============== =======================================================================================================================================================================================================================================================================================================================================================================
``title``            String          Question displayed above the control (also ``title`` on the schema property), translated with ``t()`` and rendered as inline markdown, with the ``*`` of a required control. ``label: false`` hides it. Its ``{{ expression }}`` placeholders show the value of the expression on the form data (see `rules <https://www.obiba.org/quasar-json-form/#/start/rules>`__).
``description``      String          Text under the title (also ``description`` on the schema property), translated with ``t()`` and rendered as markdown. Its ``{{ expression }}`` placeholders show the value of the expression on the form data (see `rules <https://www.obiba.org/quasar-json-form/#/start/rules>`__).
``label``            String \| false Label inside the input (also ``label`` on the schema property): floating label of an input or select, text of a toggle, upload button... Plain text, translated with ``t()``. ``false`` hides the title.
``hint``             String          Help text under the input (also ``hint`` on the schema property), translated with ``t()`` and rendered as markdown; the error messages replace it. Its ``{{ expression }}`` placeholders show the value of the expression on the form data (see `rules <https://www.obiba.org/quasar-json-form/#/start/rules>`__).
``titleClass``       String          CSS classes added to the title (``q-form-title``).
``descriptionClass`` String          CSS classes added to the description (``q-form-description``).
``hintClass``        String          CSS classes added to the hint (``q-form-hint``).
==================== =============== =======================================================================================================================================================================================================================================================================================================================================================================

.. _item_common_settings:

Common settings
---------------

The settings of every control, in the *Settings* section of the element properties:

===================== ================ ========= =====================================================================================================================================================================================================================
Setting               Type             Default   Description
===================== ================ ========= =====================================================================================================================================================================================================================
``class``             String                     CSS classes set on the root element of the control (Quasar grid classes such as ``col-md-6`` work inside a layout with ``row``).
``readonly``          Boolean          ``false`` Render the control read-only (``readOnly`` is accepted too). Also ``readOnly`` in the schema.
``format``            String                     Select a renderer when the schema ``format`` is not set (``radio``, ``checkbox``, ``images``, ``image-map``, ``geo``, ``slider``, ``range``, ``rating``, ``typeahead``, ``markdown``, ``datepicker``...).
``validationMessage`` String \| Object           Message of the renderer-level checks, translated with ``t()``: a string applies to every check of the control; in a map, ``default`` is the fallback of the named messages (``validationMessage.wordLimitError``...).
``languages``         Array \| Object            Languages of a localized string control, ``['en', 'fr']`` or ``{ en: 'English' }``; defaults to English only.
===================== ================ ========= =====================================================================================================================================================================================================================

Controls
--------

.. toctree::
   :maxdepth: 1

   text
   markdown
   localized-text
   number
   slider
   range
   rating
   toggle
   select
   radio-checkbox
   typeahead
   countries
   radio-matrix
   images
   image-map
   date
   datetime
   time
   map-location
   file-upload
   list
   computed

Layouts
-------

.. toctree::
   :maxdepth: 1

   vertical-horizontal
   grid
   group
   section-label
   tabs
   stepper

Legacy form items
-----------------

.. toctree::
   :maxdepth: 1

   legacy/index
