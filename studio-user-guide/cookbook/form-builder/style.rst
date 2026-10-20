.. _cb_fe_style:

How to style a form item?
=========================

Each element of the form can be styled with CSS classes. These classes can either be built-in or custom ones.

Step 1 - Set the CSS classes
----------------------------

In the element properties of the form builder:

* the ``class`` setting applies to the whole element (a control, a group, a layout...),
* the ``titleClass``, ``descriptionClass`` and ``hintClass`` settings (in the *JSON* section, on the UI schema element) apply to the texts of the element.

For instance, ``text-primary text-h6`` on the ``titleClass`` of a control displays its title larger and in the primary color, and ``bg-grey-2 q-pa-md`` on the ``class`` of a group gives it a grey background with some padding.

The texts of the form are rendered as Markdown: **bold**, *italic*, links and lists can be used directly in the texts. A **Label** (see :ref:`item_section_label`) also accepts HTML, for instance to display an alert box.

Built-in Style
--------------

Amber front-end applications (Studio, Collect and Visit) are based on the `Quasar <https://quasar.dev/>`_ web framework: see the `Quasar CSS classes <https://quasar.dev/style/typography>`_ for typography, `colors <https://quasar.dev/style/color-palette>`_, `spacing <https://quasar.dev/style/spacing>`_ and `grid <https://quasar.dev/layout/grid/introduction-to-flexbox>`_.

Custom Style
------------

Custom CSS classes are defined in the ``src/css/app.scss`` file of each application (see the `Amber source code <https://github.com/obiba/amber>`_), in `SCSS <https://sass-lang.com/documentation/syntax>`_ format. The applications then need to be built, for instance as Docker images, to include them.
