How to group fields?
====================

Amber has limited capabilities in terms of page layout. It is still possible to have several fields on the same page, even if they depend on each other.


Step 1 - Add a group item
-------------------------

Add an item and select the **Group** type. A name is required as it will be used a prefix to name included fields. It is also possible to define a label and a description.

A condition defined at a group level will apply to all its children (see :ref:`cb_condition`).

Step 2 - Add child items
------------------------

There are different ways of adding a item inside of a group:

* Select the group item and add a new item: it will be placed at the last position.
* Select a child item of the group and add a new item: it will be placed at the following position.
* Select an existing item and move it up/down until it is included to the group item.
* Select an existing item, cut it, select the group item and paste the item as a new child.

The position of the added item in the group can be modified by clicking on the move up or move down buttons of the item.

.. note::
  A group inside another group is currently not supported.


Step 3 - Use the children values in conditions/validations
----------------------------------------------------------

The name of the group constitutes a namespace for the included items and therefore these item names must be prefixed with the group name.

**Examples**

If the child field ``VARIABLE`` of the group ``GROUP`` is a numeric value, a validation script will look like:

.. code::

  $('GROUP.VARIABLE') > 12

Because of the group namespacing, it is possible to define items with same name in different groups:

.. code::

  $('GROUP1.VARIABLE') > $('GROUP2.VARIABLE')
