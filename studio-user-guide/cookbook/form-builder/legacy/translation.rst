.. _cb_translation:

How to translate field labels?
==============================

When the form is proposed in several languages, here are the good practices for designing the form translations with a minimum of efforts.

Step 1: Use Translation Keys
----------------------------

Whenever the label or the description (or other text to be translated) is set on an item, it is recommended to use a translation key for a better long term maintenability: typos, rewording are easier to implement. For instance use ``q1_label`` or ``nb_cigars_label`` instead of ``How many cigars do you smoke?``.

Step 2: Generate Translation Entries
------------------------------------

Once the form is ready, select the **Translations** menu on the left of the form builder and then add translation entries by selecting the **Merge with items translation keys** option. This operation will go through the designed form to retrieve the translation keys defined at Step 1.

By default all the web application languages are enabled for the form. You can restrict which form languages are to be used. Once done, there are several options for entering the translated texts:

Using the web interface
~~~~~~~~~~~~~~~~~~~~~~~

For each entry and language, select the cell in the table and type the translated text. The form is automatically saved along with the translations.

Using text file
~~~~~~~~~~~~~~~

When there are many entries, it can be more convenient to edit a file with translations. Use the form **Export** button to download the form in JSON format along with its translations. Look for the section ``i18n`` (stands for *internationalization*). Translation entries are group by languages.

.. code-block:: json

  {
    "fr": {
      "nb_cigars_label": "Combien de cigares fumez-vous ?",
      "nb_cigars_description": "Entrer 0 si vous ne fumez pas de cigares."
    },
    "en": {
      "nb_cigars_label": "How many cigars do you smoke?",
      "nb_cigars_description": "Enter 0 if you do not smoke cigars."
    }
  }


Then **Import** the form along with its translations by uploading the file.
