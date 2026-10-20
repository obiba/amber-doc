.. _cb_fe_translation:

How to translate field labels?
==============================

When the form is proposed in several languages, here are the good practices for designing the form translations with a minimum of efforts.

Step 1: Enter the texts in a first language
-------------------------------------------

The texts typed in the *Texts* section of the element properties (title, description, label, hint, choices labels, validation messages...) are stored as translation keys, generated from the key of the element: for instance ``nb_cigars.title``. They are entered in the current language of the form builder.

When a form is imported with literal texts instead of translation keys, the **Collect the texts** action of the *Translations* panel turns them into translation keys.

Step 2: Add the languages
-------------------------

In the *Translations* panel of the form builder, add the languages of the form. The panel lists the translation keys with one column per language, and highlights the missing translations (the *Missing only* filter lists them).

Then there are several options for entering the translated texts.

Using the web interface
~~~~~~~~~~~~~~~~~~~~~~~

Switch the language of the form builder and enter the texts in the *Texts* section of each element, or type them in the cells of the *Translations* table. The form is automatically saved along with the translations.

Using a CSV file
~~~~~~~~~~~~~~~~

When there are many entries, it is more convenient to send the translations to the translators as a spreadsheet. Download the translations as a CSV file: the first column is the translation key, then one column per language.

.. code-block:: text

  key,en,fr
  nb_cigars.title,How many cigars do you smoke?,Combien de cigares fumez-vous ?
  nb_cigars.description,Enter 0 if you do not smoke cigars.,Entrer 0 si vous ne fumez pas de cigares.

Then upload the completed file with **Import CSV**: the non-empty cells update or add the translations, and the new languages are added.

Step 3: Clean up
----------------

The **Remove unused translations** action removes the translation keys that are not used by any element of the form anymore, for instance after an element was removed.
