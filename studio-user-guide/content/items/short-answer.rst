.. _short_answer:

Short Answer
============

This item is for capturing a short text (one line), with a standard input field. See also the :ref:`paragraph`.

Preview
-------

.. figure:: images/short-answer.png
  :width: 600

  The short text field using standard input.

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
   * - ``Placeholder``
     - Example text included in the text area when it is empty.
   * - ``Hint``
     - Help text below the input field.
   * - ``Default``
     - The default value. Make sure it is in the right format.
   * - ``Mask``
     - | Text formatting using a mask. Below are the mask tokens:
       |
       | ``#``	Numeric
       | ``S``	Letter, a to z, case insensitive
       | ``N``	Alphanumeric, case insensitive for letters
       | ``A``	Letter, transformed to uppercase
       | ``a``	Letter, transformed to lowercase
       | ``X``	Alphanumeric, transformed to uppercase for letters
       | ``x``	Alphanumeric, transformed to lowercase for letters
       |
       | For instance the mask ``(###) ### - ####`` will format a phone number entry such as ``(514) 286 - 0768``.

Style
~~~~~

.. include:: common-style.rst
