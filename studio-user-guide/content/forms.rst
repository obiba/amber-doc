.. _forms:

Forms
=====

The forms are the heart of Amber. A form describes how the data will be collected, with a built-in support for multilanguage. The form's **schema** is made of:

* Items, which can be data input fields, structural items (group, section) or computed fields.
* Translations, which is a list of translation keys with values for each language.

Different versions of a form can be saved, which allows to safely edit a form while a version is used for data capture. Form versions also ensure that the data collected are properly described by the form that was used to collected them, avoiding variable renaming errors, options addition/removal conflicts, changes in the labels which could affect the question semantic etc.

.. image:: ../../images/amber-form-flow.png
  :width: 800

List of forms
-------------

From the list of forms the following operations are available:

Add a form
~~~~~~~~~~

When creating a form, a name is required, a description is optional. This purely informative for management purpose and will not appear when the form is administered.

It is possible to prepopulate the form with a schema, that was previously exported from another form. This is optional and can also be done later.

Delete form(s)
~~~~~~~~~~~~~~~~~

To delete several forms:

* Select one or more forms in the list,
* Press the Delete selected forms button and confirm.

You can also delete a specific form by pressing the form's Delete action button.

Single form
------------

To navigate to a form page, click on the form's name or the pencil icon. The page that is opened has two tabs:

* The schema tab, with a form item's builder and translations editor,
* The list of the form's versions.

Export
~~~~~~

Export the form's schema in text file (JSON format). Advanced users can edit this file, which can be convenient the translations section for instance.

Import
~~~~~~

Import a previously exported form schema. This operation will replace the whole tree of items.

Tag
~~~

Creates a new form revision. A comment that describes the changes in the form is recommended.

Items
~~~~~

The form items is a tree which the root is the form itself.

The following form items are available:

===================== =============== ========================================
Type                  Category        Description
===================== =============== ========================================
:ref:`auto_complete`  Select
:ref:`computed`       Misc
:ref:`date`           Temporal
:ref:`datetime`       Temporal
===================== =============== ========================================


Translations
~~~~~~~~~~~~
