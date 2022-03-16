.. _single_choice:

Single Choice
=============

The single choice item is for selecting a text. It has some "options", i.e. possible values that are proposed with radios.

This is the appropriate field for having the choices immediately visible (as opposed to :ref:`dropdown` or :ref:`auto_complete` fields), and when there are not too much options.

Preview
-------

.. figure:: images/single-choice.png
  :width: 600

  The single choice field proposes to select an option.

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
   * - ``Default``
     - The default value. A single value can be specified.
   * - ``Options``
     - The list of predefined values to be selected. For provisioning a lot of options, see :ref:`cb_large_select`

Style
~~~~~

.. include:: common-style.rst
