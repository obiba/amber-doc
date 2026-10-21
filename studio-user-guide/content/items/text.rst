.. _item_text:

Text
====

A ``{ "type": "string" }`` property renders a `QInput <https://quasar.dev/vue-components/input>`__.

The schema ``title`` is displayed above the input and the ``description`` under the title; ``label`` on the control element is the floating label of the input and ``hint`` the help text under it (see `QJsonForm <https://www.obiba.org/quasar-json-form/#/start/json-form#title-description-label-and-hint>`__). All are translated with vue-i18n when they are keys. ``required`` adds a ``*`` to the title, and ``minLength``, ``maxLength``, ``pattern`` and ``format`` are validated by AJV.

Input types
~~~~~~~~~~~

The schema ``format`` (or ``options.format``) selects the type of the input: ``email``, ``url`` / ``uri``, ``password``, ``search``, ``tel``, ``textarea``. ``email`` and ``uri`` are also validated by AJV.

Textarea
~~~~~~~~

``options.rows`` greater than 1 renders a textarea with that many rows.

Word limits
~~~~~~~~~~~

``options.wordLimit`` (``"min:max"`` or a maximum), ``wordMin`` and ``wordMax`` validate the number of words and show a word counter under the input. The messages can be set per control with ``validationMessage.wordLimitError`` / ``wordMinError`` / ``wordMaxError``, or globally with the ``error.wordLimit`` / ``error.wordMin`` / ``error.wordMax`` i18n keys.

Quasar props
~~~~~~~~~~~~

Any other option of the control is passed to ``QInput``: ``outlined``, ``filled``, ``dense``, ``clearable``, ``placeholder``, ``prefix``, ``suffix``, ``maxlength``, ``counter``, ``mask``... A control is read-only with ``readOnly: true`` on the schema property or ``options.readonly`` on the control.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

============= ============================================ ===============================================
Entry         Schema                                       UI schema
============= ============================================ ===============================================
**Text**      ``{"type": "string"}``                       ``{"type": "Control"}``
**Text area** ``{"type": "string"}``                       ``{"type": "Control", "options": {"rows": 3}}``
**Email**     ``{"type": "string", "format": "email"}``    ``{"type": "Control"}``
**URL**       ``{"type": "string", "format": "uri"}``      ``{"type": "Control"}``
**Password**  ``{"type": "string", "format": "password"}`` ``{"type": "Control"}``
============= ============================================ ===============================================

Schema
------

The schema shapes that select this renderer:

============================================== ===========================================================================================================================================
Schema                                         Description
============================================== ===========================================================================================================================================
``{ "type": "string" }``                       Any string property without a more specific renderer (``enum``, ``format: date``, ``markdown``, ``typeahead``, ``file``... have their own).
``{ "type": "string", "format": "password" }`` ``format`` selects the input type: ``text``, ``textarea``, ``password``, ``email``, ``search``, ``tel``, ``url`` / ``uri``.
============================================== ===========================================================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

=============== ================ ======== =================================================================================================================================================================================================================================
Setting         Type             Default  Description
=============== ================ ======== =================================================================================================================================================================================================================================
``type``        String           ``text`` Input type of the underlying ``QInput``, overriding the schema ``format`` (``text``, ``textarea``, ``password``, ``email``, ``search``, ``tel``, ``url``, ``number``...).
``rows``        Number                    Number of rows; when greater than 1 the input is a ``textarea``.
``placeholder`` String                    Placeholder of the input.
``mask``        String                    Input mask of ``QInput`` (``#`` a digit, ``S`` a letter, ``N`` alphanumeric...: ``(###) ### - ####``); the masked text is stored.
``wordLimit``   String \| Number          Word count limit, ``"min:max"`` or a maximum; a word counter is displayed under the input.
``wordMin``     Number                    Minimum number of words.
``wordMax``     Number                    Maximum number of words.
Other           any                       Any other option is passed as a prop to `QInput <https://quasar.dev/vue-components/input#qinput-api>`__: ``outlined``, ``filled``, ``dense``, ``clearable``, ``autocomplete``, ``maxlength``, ``prefix``, ``suffix``, ``mask``...
=============== ================ ======== =================================================================================================================================================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

============= =================== ============================================================================================================================================
Check         Message key         Description
============= =================== ============================================================================================================================================
``wordLimit`` ``error.wordLimit`` ``wordLimit: "min:max"`` not satisfied (``{min}``, ``{max}`` available in the message); ``validationMessage.wordLimitError`` on the control.
``wordMin``   ``error.wordMin``   Fewer than ``wordMin`` words (``{limit}``); ``validationMessage.wordMinError``.
``wordMax``   ``error.wordMax``   More than ``wordMax`` words (``{limit}``); ``validationMessage.wordMaxError``.
============= =================== ============================================================================================================================================

Data
----

The text as typed. An emptied input stores ``undefined`` rather than ``""``, so that ``required`` applies. Schema keywords ``minLength``, ``maxLength``, ``pattern`` and ``format`` (``email``, ``uri``...) are validated by AJV.

.. code:: json

   { "name": "Ada Lovelace" }

See also the `Text <https://www.obiba.org/quasar-json-form/#/controls/string>`__ page of the Quasar JSON Form documentation, with live examples.
