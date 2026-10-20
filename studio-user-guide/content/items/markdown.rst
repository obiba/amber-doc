.. _item_markdown:

Markdown
========

A string with ``format: "markdown"`` renders a markdown editor: a textarea with a formatting toolbar and a preview toggle.

Read-only
~~~~~~~~~

Read-only, the markdown is rendered with markdown-it and sanitized with DOMPurify.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

============ ============================================ =======================
Entry        Schema                                       UI schema
============ ============================================ =======================
**Markdown** ``{"type": "string", "format": "markdown"}`` ``{"type": "Control"}``
============ ============================================ =======================

Schema
------

The schema shapes that select this renderer:

================================================================= ===============================================================================================================
Schema                                                            Description
================================================================= ===============================================================================================================
``{ "type": "string" } + format: "markdown" (schema or options)`` Markdown editor: a textarea with a formatting toolbar (bold, italic, heading, list, link) and a preview toggle.
================================================================= ===============================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

======== ====== ======= =======================================================================================================================
Setting  Type   Default Description
======== ====== ======= =======================================================================================================================
``rows`` Number ``5``   Rows of the textarea.
Other    any            Every other option is passed as a prop to the `QInput <https://quasar.dev/vue-components/input#qinput-api>`__ textarea.
======== ====== ======= =======================================================================================================================

Data
----

The markdown text. Read-only, the rendered markdown is displayed (sanitized with DOMPurify). The toolbar titles come from the ``markdown.*`` i18n keys.

.. code:: json

   { "notes": "Some **bold** text\n\n- item" }

See also the `Markdown <https://www.obiba.org/quasar-json-form/#/controls/markdown>`__ page of the Quasar JSON Form documentation, with live examples.
