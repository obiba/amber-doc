.. _time:

Time
====

This field is for capturing a time value. It is expressed as a string in ISO 8601 format: ``hh:mm`` (2 digits hour, 2 digits minutes).

Preview
-------

.. figure:: images/time.png
  :width: 600

  The time field is in ISO 8601 format.

.. figure:: images/time-selection.png
  :width: 600

  The time selector allows to select the hour and minutes in the day. The close button can be translated.

Design
------

Definition
~~~~~~~~~~

.. include:: common-definition.rst
.. include:: common-scripts.rst

Settings
~~~~~~~~

.. list-table::
   :widths: 10 90
   :header-rows: 1

   * - Property
     - Definition
   * - ``Hint``
     - Help text below the input field.
   * - ``Close``
     - The close button's label. Use a translation key when you want to have it in several languages.
   * - ``Default``
     - The default value. Make sure it is in the right format.

Style
~~~~~

.. include:: common-style.rst
