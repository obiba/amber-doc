.. _cb_fe_backup_restore:

How to backup/restore/share a form?
===================================

In order to be adapted to the different populations, a form can have several variants. A form can also be reproduced from one study to another before being modified. Finally, a form can be backed up for further reference. This can be achieved by the following operations (from the form page):

Using Export/Import
-------------------

Export
~~~~~~

Press the **Export** button to download the form in JSON format. This file contains the form settings, the ``schema`` (the description of the data), the ``uischema`` (the layout of the controls) and the ``translations`` (see :ref:`form_engine`).

.. code-block::

  {
    "label": "Some form",
    "description": "Some form description",
    "layout": "single",
    "schema": { ... },
    "uischema": { ... },
    "translations": {
      "fr": { ... },
      "en": { ... }
    }
  }

Import
~~~~~~

The form import process consists of uploading a local file which expected format (JSON) and structure is the one you get when exporting the form. The form described in this file is self-sufficient and has no reference to the original study. A form exported in the legacy format can be imported too: it can then be converted (see :ref:`form_conversion`).

* When creating a new form: press the **Add a new form** button and select the form file to upload.
* When updating an existing form: press the **Import** button and select the form file to upload. **Important!** the current form schema, layout and translations will be overridden by the imported ones.

Using Form Revisions
--------------------

When designing a form, it is possible to "tag" the current form state into a new form revision. From the form page press the **Tag** button and provide a short comment describing the current form state. There is no limit on the number of form revisions that can be created.

From the list of form revisions, it is possible to **view** and test each form revision. Export in JSON format is also available.

Each form revision can be **reinstated**: it is similar to the import process described above (i.e. the current state of the form will be overridden).
