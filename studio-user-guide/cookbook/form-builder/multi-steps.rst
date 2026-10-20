.. _cb_fe_multi_steps:

How to split a form in pages?
=============================

A long form is easier to fill page by page.

Step 1 - Organize the form in top-level elements
------------------------------------------------

Each top-level element of the form (usually a **Group** or a **Section**, see :ref:`item_group`) will be a page. The groups and sections that have a title are also listed in the table of contents of the form.

Step 2 - Select the Multiple steps layout
-----------------------------------------

In the *Settings* panel of the form (see :ref:`form_engine_settings`), select the **Multiple steps** layout. When the form is filled in Amber Collect or Amber Visit, the pages are displayed one at a time, with **Previous** and **Next** buttons. The pages of which all the elements are hidden by their **Visible when** rules are skipped.

With the **Single page** layout, the whole form is displayed at once, with a **Go to...** table of contents.

.. tip::
  The titles of the groups and sections can show the collected data with placeholders, for instance ``Medications of {{ FIRSTNAME }}``: the table of contents shows them too.
