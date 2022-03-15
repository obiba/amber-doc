Form Items
==========

List of the items that can be included in a form.

.. toctree::
   :maxdepth: 1

   auto-complete
   computed
   date
   datetime
   dropdown
   geo-data
   group
   image-select
   multiple-choices
   number
   paragraph
   rating
   section
   short-answer
   single-choice
   slider
   time
   toggle

.. _dynamic_settings:

Dynamic settings
----------------

Some settings are expressed by a script which is evaluated at each data entry.

================== ====================================
Setting            Description
================== ====================================
``Condition``      The condition makes an item visible or not depending of other data. It is a small script which returns a logical value. True when item is visible.
``Validation``     True when item value is valid. Does not apply to items not capturing data (such as :ref:`group` or :ref:`section`).
================== ====================================

The scripting language is Javascript. It allows to express complex logic with a single line. See detailed explanations:

* :ref:`cb_condition`
* :ref:`cb_validation`
