.. _item_tabs:

Tabs
====

A JSON Forms ``Categorization`` renders its ``Category`` elements as tabs.

The tab label is the ``label`` of the category, translated with vue-i18n. Each category renders as a `Group <https://www.obiba.org/quasar-json-form/#/layouts/group>`__ without a title, so its ``description`` and ``hint`` are displayed. Rules on a control inside a tab work as anywhere else.

TabsLayout
~~~~~~~~~~

``TabsLayout`` is a lighter form: one tab per element, labelled by the ``labels`` array (or numbered).

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

======== ====== ===============================================================================================
Entry    Schema UI schema
======== ====== ===============================================================================================
**Tabs**        ``{"type": "Categorization", "elements": [{"type": "Category", "label": "", "elements": []}]}``
======== ====== ===============================================================================================

Schema
------

The schema shapes that select this renderer:

========================================================================================================= ======================================================================================================================
Schema                                                                                                    Description
========================================================================================================= ======================================================================================================================
``{ "type": "Categorization", "elements": [{ "type": "Category", "label": "...", "elements": [...] }] }`` One tab per ``Category``, labelled by its ``label`` (translated with ``t()``); the category itself renders as a group.
``{ "type": "TabsLayout", "labels": [...], "elements": [...] }``                                          One tab per element, labelled by ``labels`` (or numbered).
========================================================================================================= ======================================================================================================================

Element
-------

The keys read on the UI schema element:

============== ====== ====================================================================================
Key            Type   Description
============== ====== ====================================================================================
``elements``   Array  The tab contents.
``labels``     Array  ``TabsLayout``: the tab labels, translated with ``t()``; ``1``, ``2``... by default.
``labelClass`` String CSS classes added to every tab.
``rules``      Object ``visible`` and ``enabled`` rules apply to every tab.
============== ====== ====================================================================================

See also the `Tabs <https://www.obiba.org/quasar-json-form/#/layouts/tabs>`__ page of the Quasar JSON Form documentation, with live examples.
