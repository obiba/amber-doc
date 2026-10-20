.. _item_localized_text:

Localized Text
==============

An object with ``format: "localizedString"`` holds one value per language, entered through one input and a language selector.

The data is ``{ "en": "...", "fr": "..." }``. Switching the language selector switches every localized control of the form. A required localized string must be completed in every language, and a string emptied in every language becomes ``undefined`` so that ``required`` applies.

The languages are the ``languages`` setting of the control (English only by default), either ``['en', 'fr']`` or ``{ en: 'English', fr: 'Français' }``.

Textarea and markdown
~~~~~~~~~~~~~~~~~~~~~

``options.rows`` renders a textarea. ``options.marked: true`` (or ``format: "obibaSimpleMde"``) renders the `markdown editor <https://www.obiba.org/quasar-json-form/#/controls/markdown>`__ with a preview; read-only, the markdown is rendered.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

================== =================================================== =======================
Entry              Schema                                              UI schema
================== =================================================== =======================
**Localized text** ``{"type": "object", "format": "localizedString"}`` ``{"type": "Control"}``
================== =================================================== =======================

Schema
------

The schema shapes that select this renderer:

===================================================== ==================================================================================================
Schema                                                Description
===================================================== ==================================================================================================
``{ "type": "object", "format": "localizedString" }`` One input for the current language with a language selector (``localizedstring`` is accepted too).
``{ "type": "object", "format": "obibaSimpleMde" }``  Same, with the markdown editor.
===================================================== ==================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

============= =============== ========= ======================================================================================================================================================================
Setting       Type            Default   Description
============= =============== ========= ======================================================================================================================================================================
``rows``      Number                    Textarea with that many rows when greater than 1 (5 rows by default for the markdown editor).
``marked``    Boolean         ``false`` Markdown editor with preview instead of a plain input (also ``options.format: "markdown"``).
``languages`` Array \| Object           Languages of this control, ``['en', 'fr']`` or ``{ en: 'English' }``; defaults to ``config.languages``, then the ``languages`` prop of ``QJsonForm``, then ``['en']``.
Other         any                       Every other option is passed as a prop to `QInput <https://quasar.dev/vue-components/input#qinput-api>`__.
============= =============== ========= ======================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

============= ======================= =================================================================================================
Check         Message key             Description
============= ======================= =================================================================================================
``completed`` ``localized.completed`` A required localized string must have a value in every language; ``validationMessage.completed``.
============= ======================= =================================================================================================

Data
----

An object keyed by language code. A value emptied in every language stores ``undefined``, so that ``required`` applies. Switching the language selector switches every localized control of the form; the initial language is the vue-i18n locale when it is one of the languages. Read-only, the markdown variant renders the text.

.. code:: json

   { "title": { "en": "My study", "fr": "Mon étude" } }

See also the `Localized Text <https://www.obiba.org/quasar-json-form/#/controls/localized-string>`__ page of the Quasar JSON Form documentation, with live examples.
