How to backup/restore/share a form?
===================================

In order to be adapted to the different populations, a form can have several variants. A form can also be reproduced from one study to another before being modified. Finally, a form can be backed up for further reference. This can be achieved by the following operations (from the form page):

Using Export/Import
-------------------

Export
~~~~~~

Press the **Export** button to download the form in JSON format. This file contains the list of form items (``items`` key) and the translations (``i18n`` key, stands for *internationalization*).

.. code-block::

  {
    "label": "Some form",
    "description": "Some form description",
    "items": [ ... ],
    "i18n": {
      "fr": { ... },
      "en": { ... }
    }
  }

Import
~~~~~~

The form import process consists of uploading a local file which expected format (JSON) and structure is the one you get when exporting the form. The form described in this file is self-sufficient and has no reference to the original study.

* When creating a new form: press the **Add a new form** button and select the form file to upload.
* When updating an existing: press the **Import** button and select the form file to upload. **Important!** the current form items and translations will be overridden by the imported ones.

Using Form Revisions
--------------------

When designing a form, it is possible to "tag" the current form state into a new form revision. From the form page press the **Tag** button and provide a short comment describing the current form state. There is no limit on the number of form revisions that can be created.

From the list of form revisions, it is possible to **view** and test each form revision. Export in JSON format is also available.

Each form revision can be **reinstated**: it is similar to the import process described above (i.e. the current state of the form will be overridden).
