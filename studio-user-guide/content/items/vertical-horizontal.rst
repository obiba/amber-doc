.. _item_vertical_horizontal:

Vertical and Horizontal Layouts
===============================

``VerticalLayout`` stacks its elements, ``HorizontalLayout`` puts them side by side with equal widths.

Layouts nest freely. Without a UI schema, ``QJsonForm`` generates a ``VerticalLayout`` with one control per property of the schema.

Grid classes
~~~~~~~~~~~~

The elements are rendered as direct children of the layout root, so ``options.class`` can carry Quasar `grid classes <https://quasar.dev/layout/grid/row>`__: ``row q-col-gutter-md`` on the layout, ``col-*`` on its children. When ``row``, ``column`` or ``flex`` is present in the class, the default flex stacking of the layout is not applied. This is the equivalent of the Bootstrap ``row`` / ``col-md-6`` markup of angular-schema-form.

For a CSS grid with explicit rows, spans and named areas, see the `grid layout <https://www.obiba.org/quasar-json-form/#/layouts/grid>`__.

Rules
~~~~~

A layout accepts ``rules.visible`` and ``rules.enabled`` `rules <https://www.obiba.org/quasar-json-form/#/start/rules>`__, applied to every element it contains. The data of hidden controls is cleared.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

===================== ====== ================================================
Entry                 Schema UI schema
===================== ====== ================================================
**Vertical layout**          ``{"type": "VerticalLayout", "elements": []}``
**Horizontal layout**        ``{"type": "HorizontalLayout", "elements": []}``
===================== ====== ================================================

Schema
------

The schema shapes that select this renderer:

===================================================== =======================================================================
Schema                                                Description
===================================================== =======================================================================
``{ "type": "VerticalLayout", "elements": [...] }``   Elements stacked vertically (flex column, 10px gap).
``{ "type": "HorizontalLayout", "elements": [...] }`` Elements side by side, each taking an equal share (flex row, 20px gap).
===================================================== =======================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element).

========= ====== ======= ================================================================================================================================================================================================================================
Setting   Type   Default Description
========= ====== ======= ================================================================================================================================================================================================================================
``class`` String         CSS classes of the root element. When ``row``, ``column`` or ``flex`` is present, the default flex stacking is not applied, so Quasar grid classes work: ``row q-col-gutter-md`` on the layout and ``col-md-6`` on its children.
========= ====== ======= ================================================================================================================================================================================================================================

Element
-------

The keys read on the UI schema element:

============ ====== =======================================================================================================
Key          Type   Description
============ ====== =======================================================================================================
``elements`` Array  The child elements (layouts, groups, labels, controls), rendered as direct children of the layout root.
``rules``    Object ``visible`` and ``enabled`` rules apply to the whole layout.
============ ====== =======================================================================================================

See also the `Vertical and Horizontal Layouts <https://www.obiba.org/quasar-json-form/#/layouts/vertical-horizontal>`__ page of the Quasar JSON Form documentation, with live examples.
