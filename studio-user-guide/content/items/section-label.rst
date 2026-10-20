.. _item_section_label:

Section and Label
=================

A ``Section`` is a heading announcing the fields that follow; a ``Label`` is free markdown text.

A ``Label`` carries its content in ``text`` (JSON Forms convention). It is first resolved as a vue-i18n key, then rendered as markdown with raw HTML allowed (``<h3>``, alert ``<div>``\ s, links...), sanitized with DOMPurify. Both accept a ``rules.visible`` rule.

Section
-------

Palette
~~~~~~~

The entries of the form builder palette, and the schema property and UI schema element they create:

=========== ====== ====================================
Entry       Schema UI schema
=========== ====== ====================================
**Section**        ``{"type": "Section", "label": ""}``
=========== ====== ====================================

Schema
~~~~~~

The schema shapes that select this renderer:

========================================= ===========================================================================================
Schema                                    Description
========================================= ===========================================================================================
``{ "type": "Section", "label": "..." }`` A heading with an optional description, without children: announces the fields that follow.
========================================= ===========================================================================================

Settings
~~~~~~~~

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element).

========= ====== ======= =========================================================
Setting   Type   Default Description
========= ====== ======= =========================================================
``class`` String         CSS classes of the root element (``q-section-renderer``).
========= ====== ======= =========================================================

Element
~~~~~~~

The keys read on the UI schema element:

==================== ====== ===========================================================================================================================================================
Key                  Type   Description
==================== ====== ===========================================================================================================================================================
``label``            String The heading (``q-form-label``), translated with ``t()`` and rendered as inline markdown, with ``{{ expression }}`` placeholders; ``title`` is accepted too.
``description``      String Text under the heading, markdown, with ``{{ expression }}`` placeholders.
``labelClass``       String CSS classes added to the heading (``q-form-label``).
``descriptionClass`` String CSS classes added to the description (``q-form-description``).
``rules``            Object ``visible`` rule.
==================== ====== ===========================================================================================================================================================

Label
-----

.. _palette-1:

Palette
~~~~~~~

The entries of the form builder palette, and the schema property and UI schema element they create:

========= ====== =================================
Entry     Schema UI schema
========= ====== =================================
**Label**        ``{"type": "Label", "text": ""}``
========= ====== =================================

.. _schema-1:

Schema
~~~~~~

The schema shapes that select this renderer:

====================================== ====================================================================================================================================================
Schema                                 Description
====================================== ====================================================================================================================================================
``{ "type": "Label", "text": "..." }`` Free text: markdown with raw HTML allowed (``<h3>``, alert ``<div>``\ s...), sanitized with DOMPurify. The text is first resolved as a vue-i18n key.
====================================== ====================================================================================================================================================

.. _settings-1:

Settings
~~~~~~~~

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element).

========= ====== ======= =======================================================
Setting   Type   Default Description
========= ====== ======= =======================================================
``class`` String         CSS classes of the root element (``q-label-renderer``).
========= ====== ======= =======================================================

.. _element-1:

Element
~~~~~~~

The keys read on the UI schema element:

============== ====== =======================================================================================================
Key            Type   Description
============== ====== =======================================================================================================
``text``       String The content (JSON Forms convention), with ``{{ expression }}`` placeholders; ``label`` is accepted too.
``labelClass`` String CSS classes added to the root element.
``rules``      Object ``visible`` rule.
============== ====== =======================================================================================================

See also the `Section and Label <https://www.obiba.org/quasar-json-form/#/layouts/section-label>`__ page of the Quasar JSON Form documentation, with live examples.
