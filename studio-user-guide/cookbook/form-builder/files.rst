.. _cb_fe_files:

How to collect files?
=====================

Some data are documents rather than answers: a picture of a wound, a scan of a consent form, a laboratory report...

Step 1 - Add a File or Files control
------------------------------------

From the *Controls* menu of the form builder, add a **File** control for a single file, or a **Files** control for several files (see :ref:`item_file_upload`).

Step 2 - Restrict the files
---------------------------

* The ``accept`` setting restricts the file picker to some types: ``image/*`` for pictures, ``.pdf`` for PDF documents, ``image/*,.pdf`` for both.
* For a **Files** control, the ``minItems`` and ``maxItems`` constraints of the *Validation* section bound the number of files.
* The maximum size of a file, and the types of files accepted by the Amber server, are set by the administrator (see :ref:`api_files_settings`).

Step 3 - Test the form
----------------------

In the form builder preview, the picked files are not uploaded. Test the form in Amber Collect or Amber Visit (see :ref:`cb_testing_crf`): the picked files are kept in the browser until the case report or the interview step is saved, so that the form can be filled offline.

The files of a record can be downloaded from Amber Studio, in the case reports and interviews pages, and are included in the zip export of the records (see the case reports and interviews cookbooks).
