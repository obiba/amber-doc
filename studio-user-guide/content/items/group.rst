.. _item_group:

Group
=====

A ``Group`` is a titled block of elements, with an optional description and hint.

The ``label`` (JSON Forms convention, ``title`` is accepted too), ``description`` and ``hint`` are translated with vue-i18n and rendered as markdown. A ``Category`` inside a `Categorization <https://www.obiba.org/quasar-json-form/#/layouts/tabs>`__ renders the same way, without the title.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========= ====== =====================================================
Entry     Schema UI schema
========= ====== =====================================================
**Tab**          ``{"type": "Category", "label": "", "elements": []}``
**Group**        ``{"type": "Group", "label": "", "elements": []}``
========= ====== =====================================================

Schema
------

The schema shapes that select this renderer:

============================================================= =====================================================================
Schema                                                        Description
============================================================= =====================================================================
``{ "type": "Group", "label": "...", "elements": [...] }``    A titled block of elements.
``{ "type": "Category", "label": "...", "elements": [...] }`` The content of a ``Categorization`` tab (the tab label is ``label``).
============================================================= =====================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element).

========= ====== ======= =======================================================
Setting   Type   Default Description
========= ====== ======= =======================================================
``class`` String         CSS classes of the root element (``q-group-renderer``).
========= ====== ======= =======================================================

Element
-------

The keys read on the UI schema element:

==================== ====== ====================================================================================================================================================================
Key                  Type   Description
==================== ====== ====================================================================================================================================================================
``label``            String Title of the group (the JSON Forms convention); ``title`` is accepted too. Translated with ``t()`` and rendered as markdown, with ``{{ expression }}`` placeholders.
``description``      String Text under the title, markdown, with ``{{ expression }}`` placeholders.
``hint``             String Text after the elements, markdown, smaller and grey, with ``{{ expression }}`` placeholders.
``elements``         Array  The child elements.
``titleClass``       String CSS classes added to the title (``q-form-title``).
``descriptionClass`` String CSS classes added to the description (``q-form-description``).
``hintClass``        String CSS classes added to the hint (``q-form-hint``).
``rules``            Object ``visible`` and ``enabled`` rules apply to the whole group.
==================== ====== ====================================================================================================================================================================

See also the `Group <https://www.obiba.org/quasar-json-form/#/layouts/group>`__ page of the Quasar JSON Form documentation, with live examples.
