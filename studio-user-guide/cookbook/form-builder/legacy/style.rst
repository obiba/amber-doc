.. _cb_style:

How to style a form item?
=========================

In each form item design form, there is a **Rendering** section where you can specify some CSS classes to apply. These classes can either be built-in or custom ones.

Built-in Style
--------------

Amber front-end applications (Studio or Collect) are based on the `Quasar <https://quasar.dev/>`_ web framework. See the "Style & Identity" section in their documentation.

Custom Style
------------

A custom style can be defined in the file ``src/css/custom.scss``. The format of this style specification is `SCSS <https://sass-lang.com/documentation/syntax>`_.

See the `amber-template project <https://github.com/obiba/amber-template>`_ to integrate the custom style file into the web app built process.
