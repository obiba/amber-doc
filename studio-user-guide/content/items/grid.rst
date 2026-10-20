.. _item_grid:

Grid
====

``GridLayout`` places its elements on a `CSS grid <https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout>`__: the layout declares the columns, rows and areas, each element declares where it goes.

The ``options`` of the layout map onto the ``grid-template-*`` properties of the container: ``columns`` is a number of equal columns or a track list, ``rows`` likewise, ``areas`` names the cells, ``gap`` sets the gutters. The ``options.grid`` of an element maps onto its placement: ``column`` and ``row`` accept a line (``2``), a range (``"1 / 3"``, ``"1 / -1"`` for the full width) or a span (``"span 2"``), ``colSpan`` and ``rowSpan`` are shorthands for spans, ``area`` places the element in a named area.

Every element is wrapped in a ``.q-grid-layout__cell`` carrying its placement, so any renderer, including a custom one, can be placed. The cell of an element hidden by a `rule <https://www.obiba.org/quasar-json-form/#/start/rules>`__ is removed from the flow.

Breakpoints
~~~~~~~~~~~

``columns``, ``rows``, ``areas``, the gaps and every placement value also accept a `Quasar breakpoint <https://quasar.dev/style/breakpoints>`__ map, resolved against the screen width like the ``col-md-*`` classes: the value of the largest breakpoint not wider than the screen applies, and none below the smallest one. Fluid grids need no breakpoints at all: ``"columns": "repeat(auto-fit, minmax(240px, 1fr))"``.

Flex grid
~~~~~~~~~

The Quasar ``row`` / ``col-*`` classes remain available on the `vertical and horizontal layouts <https://www.obiba.org/quasar-json-form/#/layouts/vertical-horizontal>`__ for a flexbox grid, the equivalent of the Bootstrap markup of angular-schema-form.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

======== ====== =====================================================================
Entry    Schema UI schema
======== ====== =====================================================================
**Grid**        ``{"type": "GridLayout", "options": {"columns": 2}, "elements": []}``
======== ====== =====================================================================

Schema
------

The schema shapes that select this renderer:

============================================================================ ===================================================================================================
Schema                                                                       Description
============================================================================ ===================================================================================================
``{ "type": "GridLayout", "options": { "columns": 3 }, "elements": [...] }`` A CSS grid container: ``options`` declare the grid, ``options.grid`` of each element its placement.
============================================================================ ===================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element).

============= ================ ======= ============================================================================================================================================================================================================================================
Setting       Type             Default Description
============= ================ ======= ============================================================================================================================================================================================================================================
``columns``   Number \| String         ``grid-template-columns``: a number of equal columns (``repeat(n, minmax(0, 1fr))``) or a track list (``200px 1fr``, ``repeat(auto-fit, minmax(240px, 1fr))``).
``rows``      Number \| String         ``grid-template-rows``, same values as ``columns``.
``areas``     Array \| String          ``grid-template-areas``: one string per row (``["title title", "year month"]``), or a single string of comma separated rows (``title title, year month``); ``.`` for an empty cell.
``gap``       Number \| String         Row and column gap, in px when a number. Defaults to the 10px row / 20px column gaps of the flex layouts.
``rowGap``    Number \| String         ``row-gap``, wins over ``gap``.
``columnGap`` Number \| String         ``column-gap``, wins over ``gap``.
``autoFlow``  String                   ``grid-auto-flow``: ``row``, ``column``, ``dense``, ``row dense``...
``align``     String                   ``align-items`` of the cells: ``stretch`` (default), ``start``, ``center``, ``end``.
``justify``   String                   ``justify-items`` of the cells.
``class``     String                   CSS classes of the root element.
``grid``      Object                   On each **element** of the layout: its placement. ``column`` / ``row`` (``2``, ``"1 / 3"``, ``"span 2"``), ``colSpan`` / ``rowSpan`` (numbers), ``area`` (name from ``areas``), ``align`` / ``justify`` (``align-self`` / ``justify-self``).
============= ================ ======= ============================================================================================================================================================================================================================================

Element
-------

The keys read on the UI schema element:

============ ====== ==========================================================================================================================
Key          Type   Description
============ ====== ==========================================================================================================================
``elements`` Array  The child elements (layouts, groups, labels, controls), each wrapped in a ``.q-grid-layout__cell`` carrying its placement.
``rules``    Object ``visible`` and ``enabled`` rules apply to the whole layout.
============ ====== ==========================================================================================================================

See also the `Grid <https://www.obiba.org/quasar-json-form/#/layouts/grid>`__ page of the Quasar JSON Form documentation, with live examples.
