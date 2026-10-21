.. _item_file_upload:

File Upload
===========

The ``file`` and ``files`` formats render an upload button and the list of the uploaded files.

============================== ==============================================================
Schema                         Data
============================== ==============================================================
``type: string, format: file`` the identifier of the uploaded file
``type: array, format: files`` a list of file items ``[{ id, fileName, size, contentType }]``
============================== ==============================================================

In Amber Collect and Amber Visit, the picked files are stored in the browser, and uploaded to the Amber server when the case report or the interview step is saved, so that a form with files can be filled offline. The files are then attached to their record: they are deleted with it and included in the records export. The maximum size and the accepted types of the files are set by the Amber server (see the :ref:`files settings <api_files_settings>`). In the form previews of Amber Studio, the uploads are simulated.

The title and description are displayed above the list, the hint under it, and the ``label`` sets the upload button label. ``minItems`` / ``maxItems`` from the schema (or the ``min`` / ``max`` rules) bound the number of files; ``multiple`` defaults to true unless ``maxItems`` is 1. The ``accept`` setting restricts the file picker to some types (``.pdf``, ``image/*``...).

Palette
-------

The entries of the form builder palette, and the schema property and UI schema element they create:

========= ======================================== =======================
Entry     Schema                                   UI schema
========= ======================================== =======================
**File**  ``{"type": "string", "format": "file"}`` ``{"type": "Control"}``
**Files** ``{"type": "array", "format": "files"}`` ``{"type": "Control"}``
========= ======================================== =======================

Schema
------

The schema shapes that select this renderer:

=========================================================== ====================================================================================================
Schema                                                      Description
=========================================================== ====================================================================================================
``{ "type": "string", "format": "file" }``                  A single file, the data is its path.
``{ "type": "array", "format": "files" }``                  A list of file items.
``{ "type": "object", "format": "files" \| "obibaFiles" }`` An object holding the list under ``itemsKey`` (``obibaFiles`` for that format, ``files`` otherwise).
=========================================================== ====================================================================================================

Settings
--------

The settings of the renderer, in the *Settings* section of the element properties (stored in the ``options`` of the UI schema element), in addition to the :ref:`common settings <item_common_settings>`.

===================== =============== ======= ===========================================================================================================================
Setting               Type            Default Description
===================== =============== ======= ===========================================================================================================================
``multiple``          Boolean                 Several files; defaults to true unless ``maxItems`` is 1 (always false for a path control).
``accept``            String                  Accepted file types of the file picker (``.pdf``, ``image/*``...); ``acceptedFileTypes`` (string or array) is accepted too.
``acceptedFileTypes`` String \| Array         Alias of ``accept`` (angular-schema-form convention), a string or an array of types.
``emptyMessage``      String                  Text displayed read-only when there is no file; defaults to the ``files.empty`` message.
===================== =============== ======= ===========================================================================================================================

Element
-------

The keys read on the UI schema element:

========= ====== =============================================================================================================
Key       Type   Description
========= ====== =============================================================================================================
``label`` String Label of the upload button (also ``label`` on the schema property); defaults to the ``files.upload`` message.
========= ====== =============================================================================================================

Validation
----------

The checks made by the renderer, in addition to the schema validation (see :ref:`Validation <form_engine_validation>`):

================ ================== =============================================================================================================
Check            Message key        Description
================ ================== =============================================================================================================
``missingFiles`` ``files.missing``  The control is required and has no file (once the data exists); ``validationMessage.missingFiles``.
``minItems``     ``files.minItems`` Object controls: fewer files than ``minItems`` (schema, or the ``min`` rule); ``validationMessage.minItems``.
``maxItems``     ``files.maxItems`` Object controls: more files than ``maxItems``; ``validationMessage.maxItems``.
================ ================== =============================================================================================================

Data
----

A ``file`` control stores the identifier of the uploaded file, a ``files`` control the list of the file items ``{ id, fileName, size, contentType }``. The errors are reported with the ``files`` keyword.

.. code:: json

   {
     "picture": "6718f0c2a3b4c5d6e7f80912",
     "attachments": [{ "id": "6718f0c2a3b4c5d6e7f80913", "fileName": "protocol.pdf", "size": 245760, "contentType": "application/pdf" }]
   }

See also the `File Upload <https://www.obiba.org/quasar-json-form/#/controls/file-upload>`__ page of the Quasar JSON Form documentation, with live examples.
