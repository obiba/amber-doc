.. _item_stepper:

Stepper
=======

``StepperLayout`` renders one step per element with Continue and Back buttons.

The step titles come from ``labels`` and the icons from ``icons``, both optional. The navigation buttons use the ``continue`` and ``back`` i18n keys of the application. The stepper does not block navigation on validation errors: the form ``errors`` model tells whether the data is valid.

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

=========== ====== ===========================================================
Entry       Schema UI schema
=========== ====== ===========================================================
**Stepper**        ``{"type": "StepperLayout", "labels": [], "elements": []}``
=========== ====== ===========================================================

Schema
------

The schema shapes that select this renderer:

=================================================================== ============================================================================================
Schema                                                              Description
=================================================================== ============================================================================================
``{ "type": "StepperLayout", "labels": [...], "elements": [...] }`` One step per element, with Continue / Back navigation (``continue`` and ``back`` i18n keys).
=================================================================== ============================================================================================

Element
-------

The keys read on the UI schema element:

============== ====== =========================================================================
Key            Type   Description
============== ====== =========================================================================
``elements``   Array  The step contents.
``labels``     Array  The step titles, translated with ``t()``; ``1``, ``2``... by default.
``icons``      Array  One icon name per step (ignored unless there is exactly one per element).
``labelClass`` String CSS classes added to the stepper.
``rules``      Object ``enabled`` rule applies to every step.
============== ====== =========================================================================

See also the `Stepper <https://www.obiba.org/quasar-json-form/#/layouts/stepper>`__ page of the Quasar JSON Form documentation, with live examples.
