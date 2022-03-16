.. _group:

Group
=====

The group item is a structural item: it does not collect any data, it only contains other items. As a consequence, this item will not appear in the exported data dictionary.

This item is appropriate when the form is rendered in multiple pages and several items are to be displayed in the same page. See also :ref:`section`.

Preview
-------

.. figure:: images/group.png
  :width: 600

  The group is a title followed by a paragraph and the list of child items.

Design
------

Definition
~~~~~~~~~~

.. list-table::
   :widths: 10 90
   :header-rows: 1

   * - Property
     - Definition
   * - ``Type``
     - The type of item (see above).
   * - ``Name``
     - | The name of the group is not visible. It is used as a prefix to the child items variable name. For instance if the group name is ``NUTRITION`` and
       | if it contains an item with name ``SUGAR``, the collected data of this child item will be accessible with the full name ``NUTRITION.SUGAR``.
   * - ``Label``
     - The label is usually a question or a title.
   * - ``Description``
     - The description gives some guidance about how to enter data, what are their meaning etc.
   * - ``Condition``
     - | The condition makes the group and its child items visible or not, depending of other data. It is a small script which returns a logical value: ``true`` when item is visible.
       | When no condition is specified (which is the default), the group and its child item are visible. Each child item can have its own condition rule as well.
       | See :ref:`cb_condition`

Style
~~~~~

.. list-table::
   :widths: 10 90
   :header-rows: 1

   * - Property
     - Definition
   * - ``Label class``
     - CSS class to apply to the group title. Default is ``text-h5``. See :ref:`cb_style`
   * - ``Description class``
     - CSS class to apply to the group description. Default is ``text-subtitle2 text-grey-8``.
