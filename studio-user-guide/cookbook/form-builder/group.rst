.. _cb_fe_group:

How to group fields?
====================

The layouts of the form builder arrange the fields on the page: groups, columns, grids, tabs, steps...

Step 1 - Add a Group
--------------------

From the *Layouts* menu of the form builder, add a **Group** (see :ref:`item_group`) and enter its title, and optionally its description and hint, in the *Texts* section. Groups can be nested.

A **Visible when** rule defined on a group applies to all its elements (see :ref:`cb_fe_condition`).

Step 2 - Add the fields
-----------------------

Select the group in the outline and add the controls from the *Controls* menu: they are added inside the group. The existing elements can also be moved into the group, or reordered, by drag and drop in the outline.

A group arranges the fields on the page, it does not change the data: the keys of the fields must be unique in the form, and the fields are named by their key in the expressions. The forms converted from the legacy format are an exception: their groups are kept as nested objects in the data, and their fields are named ``GROUP.VARIABLE`` in the expressions (see :ref:`form_conversion`).

To repeat a set of fields (for instance, one entry per medication), use a **List** control (see :ref:`item_list`).

Step 3 - Arrange the fields in columns
--------------------------------------

Inside a group, the fields are stacked. To place them side by side:

* add a **Horizontal layout** in the group: its elements are displayed side by side with equal widths,
* or set the ``class`` setting of the group to ``row q-col-gutter-md`` and the ``class`` setting of each field to a column size, such as ``col-md-6`` (half of the width on medium and large screens, full width on small screens),
* or add a **Grid** for columns, rows and spans adapted to the screen size (see :ref:`item_grid`).

Other layouts are available: **Tabs** (or a **Categorization** of **Tab** elements), to display groups of fields in tabs, and **Stepper**, to display them one step at a time.
