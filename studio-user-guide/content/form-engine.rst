.. _form_engine:

Form Engine
===========

The forms of Amber are rendered by a form engine based on `JSON Forms <https://jsonforms.io/>`_, the `Quasar JSON Form <https://www.obiba.org/quasar-json-form/>`_ library. A new form is created in this format and edited with a visual **form builder**. The forms designed with the previous form engine (a tree of :ref:`items <forms_items>` with their translations) are still supported and can be :ref:`converted <form_conversion>` to the new one.

The form engine is used everywhere a form is displayed: the form previews of Amber Studio, the case report forms of Amber Collect and the interview steps of Amber Visit. The data collected have the same shape in both formats, so the records already collected are read and exported as before.

.. note::
  This page gives an overview of the possibilities of the form engine. Each control, layout and rule is described in detail, with live examples, in the `Quasar JSON Form documentation <https://www.obiba.org/quasar-json-form/>`_.

Form Schema
-----------

A form schema is a self-contained bundle made of:

* **Schema**: a `JSON Schema <https://json-schema.org/>`_ (draft 7) describing the data: one property per variable, with its type (``string``, ``number``, ``integer``, ``boolean``, ``object``, ``array``), its format, its allowed values (``enum`` or ``oneOf``) and its validation keywords (``required``, ``minimum``, ``maxLength``, ``pattern``...). The data dictionary of the collected data is built from this schema.
* **UI schema**: a `JSON Forms UI schema <https://jsonforms.io/docs/uischema>`_ describing how the data are captured: the layouts (vertical, horizontal, grid, group, tabs, stepper...), the labels and sections, and the controls pointing at a schema property through a ``scope`` (for instance ``#/properties/age``). The ``options`` of a control select a specific renderer and configure it.
* **Translations**: the texts of the form, keyed by language. Every title, description, label, hint, option label and validation message of the schema and the UI schema is a translation key.

Amber adds some form-level settings to this bundle (see :ref:`form_engine_settings`).

Example of an exported form schema (simplified):

.. code-block:: json

  {
    "label": "baseline.title",
    "idLabel": "Participant ID",
    "layout": "single",
    "schema": {
      "type": "object",
      "properties": {
        "age": { "type": "integer", "title": "age.title", "minimum": 18 },
        "smoker": { "type": "boolean", "title": "smoker.title" },
        "cigarettes": { "type": "integer", "title": "cigarettes.title" }
      },
      "required": ["age"]
    },
    "uischema": {
      "type": "VerticalLayout",
      "elements": [
        { "type": "Control", "scope": "#/properties/age" },
        { "type": "Control", "scope": "#/properties/smoker" },
        { "type": "Control", "scope": "#/properties/cigarettes", "rules": { "visible": "smoker == true" } }
      ]
    },
    "translations": {
      "en": { "age.title": "Age", "smoker.title": "Do you smoke?", "cigarettes.title": "How many cigarettes per day?" },
      "fr": { "age.title": "Âge", "smoker.title": "Fumez-vous ?", "cigarettes.title": "Combien de cigarettes par jour ?" }
    }
  }

.. tip::
  A complete example covering all the controls and layouts, the `DemoForm <https://github.com/obiba/amber/blob/main/examples/DemoForm-schema.json>`_, can be imported in a form to explore the possibilities of the form engine.

Form Design
-----------

The **Schema** tab of a form has two panels: the form **Settings** and the form **Items**. The form is saved automatically while it is edited (the time of the last save is displayed next to the save button). The *Export*, *Import* and *Tag* actions are the same as for any form (see :ref:`forms`).

.. _form_engine_settings:

Settings
~~~~~~~~

The form-level settings, which are not part of the JSON Forms schema:

========================== =========================================================================
Setting                    Description
========================== =========================================================================
``Title``                  The title of the form, displayed above the form when it is administered.
``Description``            The description of the form.
``Copyright``              The copyright holder of the form.
``License``                The license of the form: one of the Creative Commons licenses or a license defined in the Amber Studio :ref:`settings <app_settings>`.
``Layout``                 *Single page*: all the form is displayed at once. *Multiple steps*: each top-level element of the UI schema is a page. The pages of which all the elements are hidden by their visibility rules are skipped.
``ID label``               The label of the patient or participant's identifier field (case report forms).
``ID description``         The description of the identifier field.
``ID mask``                The input mask of the identifier field (for instance ``####`` for 4 digits).
``ID validation``          The validation rule of the identifier field.
``ID validation message``  The message displayed when the identifier is not valid.
========================== =========================================================================

Form Builder
~~~~~~~~~~~~

The form builder (`QJsonFormBuilder <https://www.obiba.org/quasar-json-form/#/builder/overview>`_) edits the schema, the UI schema and the translations of the form together. It is made of:

* **Outline**: the tree of the form, with a palette of layouts and controls. The elements are reordered and moved into another layout by drag and drop.
* **Properties** of the selected element: its name (the variable name; renaming it updates the nested controls and lists the rules still mentioning the old name), whether it is required, its texts in the current language, its choices, the settings of its renderer, the validation keywords of its property, its :ref:`rules <form_engine_rules>` (checked against the names of the fields of the form) and the raw JSON of the element and of the property for anything else.
* **Preview**: the form as it will be rendered, with a language switch, a read-only toggle and the collected data and errors. The file controls of the preview do not upload anything.
* **Translations**: a table of the translation keys with one column per language, the missing translations highlighted. Languages can be added. The *Collect the texts* action turns the literal texts of an imported form into translation keys. The table can be downloaded as a CSV file (``key`` then one column per language) for the translators, and uploaded back.
* **Source**: the schema, the UI schema and the translations, editable as JSON.

The texts typed in the builder are stored as translation keys generated from the position of the element, so that they stay readable and stable:

=============================================== ===========================================
Text                                            Translation key
=============================================== ===========================================
Title and description of a property             ``name.title``, ``name.description``
Label and hint of a control                     ``name.label``, ``name.hint``
A property in a list of objects                 ``contacts.items.email.title``
Option labels                                   ``role.options.editor``
Messages of the validation rules                ``name.validation.0``
Label of a group or a section                   ``group.1.label``, ``section.1.description``
=============================================== ===========================================

A hand-written schema is preserved: the keywords that the builder does not understand stay attached to their element and are saved as they were.

Texts
-----

Every control displays its texts the same way, questionnaire style:

* the **title**, above the control, in bold, with a ``*`` when the control is required,
* the **description**, under the title,
* the **label**, inside the input (floating label of a text input, text of a toggle, label of an upload button),
* the **hint**, under the input, replaced by the error message when the value is not valid.

The texts are translated and rendered as `Markdown <https://www.markdownguide.org/basic-syntax/>`__: bold, italic, links, lists etc. can be used.

**Placeholders**: a ``{{ expression }}`` in a text shows the value of the :ref:`expression <form_engine_expressions>` with the form data, for instance ``Hello {{ firstname }}, how old are you?``. The text is updated as the data change. Placeholders can be used in the titles, descriptions, labels and hints of the controls, groups and sections, and in the labels of the tabs and of the steps.

Controls
--------

The renderer of a control is selected from the type and the format of its schema property, and from the ``format`` option of the control in the UI schema. Each control and layout, with its settings, is described in :ref:`form_items`.

.. list-table::
   :header-rows: 1
   :widths: 20 35 45

   * - Control
     - Schema
     - Description
   * - `String <https://www.obiba.org/quasar-json-form/#/controls/string>`_
     - ``string``, formats ``email``, ``uri``, ``tel``, ``password``, ``textarea``
     - Text input, or text area with the ``rows`` option. Supports input masks (``mask`` option), word limits (``wordLimit``, ``wordMin``, ``wordMax``) and any `QInput <https://quasar.dev/vue-components/input>`_ property (``placeholder``, ``prefix``, ``suffix``, ``counter``...).
   * - `Markdown <https://www.obiba.org/quasar-json-form/#/controls/markdown>`_
     - ``string``, format ``markdown``
     - Markdown editor with a formatting toolbar and a preview.
   * - `Localized string <https://www.obiba.org/quasar-json-form/#/controls/localized-string>`_
     - ``object``, format ``localizedString``
     - One text per language, entered through a language selector.
   * - `Number <https://www.obiba.org/quasar-json-form/#/controls/number>`_
     - ``number``, ``integer``
     - Numeric input, validated by ``minimum``, ``maximum``, ``multipleOf``...
   * - `Slider <https://www.obiba.org/quasar-json-form/#/controls/slider>`_
     - ``integer``, option ``format: slider``
     - Gradual numeric value, rendered as a slider.
   * - `Range <https://www.obiba.org/quasar-json-form/#/controls/range>`_
     - ``object``, format ``range``
     - A ``{ min, max }`` pair of numbers, selected with a two-ends slider.
   * - `Rating <https://www.obiba.org/quasar-json-form/#/controls/rating>`_
     - ``integer``, option ``format: rating``
     - Gradual numeric value, rendered as icons (stars, hearts...).
   * - `Toggle <https://www.obiba.org/quasar-json-form/#/controls/toggle>`_
     - ``boolean``
     - True or false.
   * - `Select <https://www.obiba.org/quasar-json-form/#/controls/select>`_
     - ``enum`` or ``oneOf``; ``array`` with ``uniqueItems`` for a multiple selection
     - Dropdown menu. Each option of a ``oneOf`` can have its own visibility rule, for dependent selections.
   * - `Radio and checkbox <https://www.obiba.org/quasar-json-form/#/controls/options>`_
     - option ``format: radio``, ``checkbox`` or ``toggle``
     - The options of a selection as radio buttons (single choice) or checkboxes (multiple choices).
   * - `Typeahead <https://www.obiba.org/quasar-json-form/#/controls/typeahead>`_
     - ``string`` (or ``array``), format ``typeahead``
     - Input with filtered suggestions, for long lists of options. Free text can be accepted (``editable`` option).
   * - `Countries <https://www.obiba.org/quasar-json-form/#/controls/countries>`_
     - format ``countries``
     - Searchable selection of ISO 3166-1 alpha-3 country codes.
   * - `Radio matrix <https://www.obiba.org/quasar-json-form/#/controls/radio-matrix>`_
     - ``object``, format ``radio-matrix``
     - Items as rows and values as radio columns (Likert scale), or one checkbox per item.
   * - `Images <https://www.obiba.org/quasar-json-form/#/controls/images>`_
     - option ``format: images``
     - The options of a selection as a grid of images to click, single or multiple, optionally ordered.
   * - `Image map <https://www.obiba.org/quasar-json-form/#/controls/image-map>`_
     - option ``format: image-map``
     - The options of a selection as clickable areas of a single image (body map, anatomical chart...).
   * - `Date <https://www.obiba.org/quasar-json-form/#/controls/date>`_
     - ``string``, format ``date``, ``year-month``, ``datepicker``
     - Date input with a date picker, ``YYYY-MM-DD`` (ISO 8601). Bounds can be given as options or as ``min`` / ``max`` rules referring to another field.
   * - `Date and time <https://www.obiba.org/quasar-json-form/#/controls/datetime>`_
     - ``string``, format ``date-time``
     - Date and time input, ``YYYY-MM-DD HH:mm``.
   * - `Time <https://www.obiba.org/quasar-json-form/#/controls/time>`_
     - ``string``, format ``time``
     - Time input with a time picker, ``HH:mm`` (``fulltime`` for the seconds).
   * - `Geo <https://www.obiba.org/quasar-json-form/#/controls/geo>`_
     - ``object``, format ``geo``
     - A map on which a point, a line or a polygon is drawn (`GeoJSON <https://datatracker.ietf.org/doc/html/rfc7946>`_ geometry). The *My position* button uses the location of the device.
   * - `File upload <https://www.obiba.org/quasar-json-form/#/controls/file-upload>`_
     - format ``file`` or ``files``
     - Upload of one or more files (see :ref:`form_engine_files`).
   * - `List <https://www.obiba.org/quasar-json-form/#/controls/list>`_
     - ``array`` of objects or of values
     - Repeated items, with add, remove and reorder buttons. The number of items can be bounded (``minItems``, ``maxItems`` or ``min`` / ``max`` rules).
   * - `Computed <https://www.obiba.org/quasar-json-form/#/controls/computed>`_
     - format ``computed``
     - Value computed from the other data with a ``compute`` rule (a score, a BMI...). Hidden by default, the ``show`` option displays it.

Layouts
-------

The UI schema arranges the controls with layouts, which can be nested freely:

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Layout
     - Description
   * - `VerticalLayout, HorizontalLayout <https://www.obiba.org/quasar-json-form/#/layouts/vertical-horizontal>`_
     - Elements stacked, or side by side with equal widths. The `Quasar grid classes <https://quasar.dev/layout/grid/row>`_ (``row``, ``col-md-6``...) can be applied with the ``class`` option for responsive columns.
   * - `GridLayout <https://www.obiba.org/quasar-json-form/#/layouts/grid>`_
     - Elements placed on a CSS grid with columns, rows, spans and named areas, adapted to the screen size.
   * - `Group <https://www.obiba.org/quasar-json-form/#/layouts/group>`_
     - Titled block of elements, with a description and a hint. With the *Multiple steps* layout, each top-level group is a page and appears in the table of contents.
   * - `Section and Label <https://www.obiba.org/quasar-json-form/#/layouts/section-label>`_
     - A heading announcing the fields that follow, or a free text (Markdown, HTML allowed) such as an instruction or a warning.
   * - `Categorization, TabsLayout <https://www.obiba.org/quasar-json-form/#/layouts/tabs>`_
     - Elements displayed in tabs.
   * - `StepperLayout <https://www.obiba.org/quasar-json-form/#/layouts/stepper>`_
     - One step per element, with *Continue* and *Back* buttons.

The ``class``, ``titleClass``, ``descriptionClass`` and ``hintClass`` options apply CSS classes (for instance the `Quasar typography and color classes <https://quasar.dev/style/typography>`_) to an element and its texts.

.. _form_engine_rules:

Rules
-----

The dynamic behavior of a form is declared with rules, on the schema property or on the UI schema element (the latter wins). A rule is an :ref:`expression <form_engine_expressions>` evaluated with the form data, each time the data change.

.. code-block:: json

  { "type": "Control", "scope": "#/properties/city", "rules": { "visible": "country == 'CA'" } }

================= ================================================================================
Rule              Effect
================= ================================================================================
``visible``       The element is hidden when false; the data of a hidden control are cleared. Applies to controls, layouts, groups, sections and labels, and to the options of a selection.
``enabled``       The element is disabled when false; as when hidden, its data are cleared.
``required``      The control is required while true (replaces the static ``required`` of the property).
``validation``    A list of ``{ "expr": "...", "message": "..." }``: each expression must be true, otherwise the message (translated) is displayed.
``min``, ``max``  Bounds of a date, of the number of items of a list or of the number of uploaded files, possibly computed from another field.
``compute``       The value of a computed control.
================= ================================================================================

Example of validation rules:

.. code-block:: json

  {
    "rules": {
      "validation": [
        { "expr": "isEmpty(weight) || weight > 30", "message": "weight.validation.0" },
        { "expr": "isEmpty(visit) || visit <= today()", "message": "visit.validation.0" }
      ]
    }
  }

.. _form_engine_expressions:

Expressions
~~~~~~~~~~~

The expressions are a safe subset of JavaScript (see `Rules <https://www.obiba.org/quasar-json-form/#/start/rules>`_):

* the fields are named by their path in the form data, ``age`` or ``address.city`` for a field nested in a group; a missing value is ``undefined`` (no error),
* string, number, ``true``, ``false``, ``null``, ``undefined`` and array literals,
* arithmetic (``+``, ``-``, ``*``, ``/``, ``%``), comparisons (``==``, ``!=``, ``===``, ``!==``, ``<``, ``<=``, ``>``, ``>=``), ``&&``, ``||``, ``!`` and the ``cond ? a : b`` ternary,
* calls of the following functions:

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Function
     - Description
   * - ``isEmpty(v)``, ``isNotEmpty(v)``
     - Null, undefined or empty string
   * - ``isNull(v)``, ``isUndefined(v)``
     - Null or undefined; undefined only
   * - ``isBoolean(v)``, ``isNumber(v)``, ``isString(v)``
     - Type checks
   * - ``truthy(v)``
     - JavaScript truthiness
   * - ``ifElse(cond, a, b)``
     - ``a`` when ``cond`` is true, else ``b``
   * - ``length(v)``
     - Length of a string or of a list
   * - ``get(v, i)``
     - Element ``i`` of a string or of a list
   * - ``contains(list, v)``
     - The list (or string) contains ``v``: ``contains(symptoms, 'fever')``
   * - ``inArray(v, a, b, ...)``
     - ``v`` is one of the arguments
   * - ``startsWith(s, p)``, ``endsWith(s, p)``
     - String prefix / suffix
   * - ``matches(s, pattern)``
     - Regular expression test: ``matches(code, '^[A-Z]{2}[0-9]{4}$')``
   * - ``wordCount(s)``
     - Number of words
   * - ``now()``
     - Current time in milliseconds
   * - ``today()``
     - Current date as ``YYYY-MM-DD``
   * - ``currentYear()``, ``currentMonth()``, ``currentDay()``, ``currentWeekday()``
     - Current year, month (1 to 12), day of the month, day of the week (0 is Sunday)
   * - ``currentHour()``, ``currentMinute()``, ``currentSecond()``
     - Current time parts
   * - ``parseInt(s)``, ``parseFloat(s)``
     - Number parsed from a string
   * - ``parseDate(s)``
     - Milliseconds of a date: ``parseDate(birth) < now()``
   * - ``map(v, mapping, undef)``
     - Recodes a value with an object (``map(sex, { "1": "M", "2": "F", "*": "U" })``) or with thresholds (``map(age, [18, 'minor', 65, 'adult', 65, 'senior'])``: ``minor`` below 18, ``adult`` below 65, ``senior`` from 65)

.. note::
  An expression that cannot be evaluated counts as false, except for a ``visible`` rule: the element stays visible. As in JavaScript, ``undefined > 3`` is false, so the validation rule of an optional field is usually guarded: ``isEmpty(score) || score % 2 == 0``.

.. _form_engine_validation:

Validation
----------

The data are validated against the schema (``required``, ``minLength``, ``maxLength``, ``pattern``, ``format``, ``minimum``, ``maximum``, ``multipleOf``, ``minItems``, ``maxItems``, ``uniqueItems``...), by the controls themselves (word limits, date bounds, localized strings completed in every language, number of files, every row of a radio matrix answered) and by the ``validation`` rules. The errors are displayed under the controls, and listed when the form is validated (for instance when a case report or an interview step is completed).

The error messages are translated. A form can carry its own messages in its translations, for a specific control (``<name>.error.<keyword>``, for instance ``age.error.minimum``) or for all the controls (``error.<keyword>``, for instance ``error.required``), with the parameters of the error available for interpolation (``{limit}``, ``{pattern}``...). The checks of the controls read their message from the ``validationMessage`` option of the control.

.. _form_engine_files:

Files
-----

The ``file`` and ``files`` controls upload files, such as pictures, scans or documents, which are attached to the case report or to the interview:

* the files are stored by the Amber server (encrypted when data encryption is enabled), deleted with their record and included in the records export (see the ``files`` :ref:`server settings <api_files_settings>` for the maximum size and the accepted types),
* in Amber Collect and Amber Visit, the picked files are kept in the browser while offline and uploaded when the case report or the interview step is saved,
* in Amber Studio, the files of the records can be downloaded from the case reports and interviews pages; the form previews simulate the uploads.

The number of files can be bounded with ``minItems`` / ``maxItems`` in the schema, or with the ``min`` / ``max`` rules.

Translations
------------

The form carries its own translations: the languages of the form are the languages of its ``translations``. A text is looked up in the language of the user (``fr-CA`` also tries ``fr``), then in English. A text which is not a translation key is displayed as is.

The translations are edited in the *Translations* panel of the form builder, or exchanged with translators as a CSV file.

.. _form_conversion:

Conversion of a Legacy Form
---------------------------

A form designed with the previous form engine has a *Convert* action. The conversion dialog displays the current form and the converted form side by side, together with the conversion diagnostics (the expressions that could not be translated, for instance). Both forms can be filled in, and the data copied from one to the other, to check that they collect the same data.

*Apply conversion* replaces the form draft by the converted form; the published revisions are not modified, so the case report forms and interview designs using them are not affected until a new revision is tagged and selected.

The conversion follows these rules (see `Migrating from Amber forms <https://www.obiba.org/quasar-json-form/#/migration/amber>`_):

=================================================== ==========================================================
Legacy item                                         Converted to
=================================================== ==========================================================
Short answer, Paragraph                             String (text area with 3 rows)
Number                                              Number
Slider, Rating                                      Integer with the slider / rating format
Single choice, Dropdown                             Selection rendered as radio buttons
Multiple choices, Dropdown with multiple selection  Multiple selection rendered as checkboxes
Auto complete                                       Typeahead
Image select                                        Image map
Toggle                                              Toggle
Date, Date time, Time                               Date, Date and time, Time
Geo data                                            Geo (a list of them for multiple features)
Computed                                            Computed, with a ``compute`` rule
Section                                             Section
Group                                               Group (nested object in the data)
=================================================== ==========================================================

The *Condition*, *Required*, *Disabled*, *Validation* and *Compute* scripts become the ``visible``, ``required``, ``enabled``, ``validation`` and ``compute`` rules: ``$('GROUP.ITEM')`` becomes ``GROUP.ITEM``, ``list.includes(v)`` becomes ``contains(list, v)``, ``Date.now()`` becomes ``now()`` etc. A script that cannot be expressed as a rule (a block of statements, a method call) is reported in the diagnostics and dropped: it then needs to be rewritten in the form builder.

.. tip::
  Before converting the forms of a production database, the conversion can be tried on a database export to report the diagnostics without modifying anything (see the `form conversion dry run <https://github.com/obiba/amber/tree/main/studio#form-conversion-dry-run>`_).
