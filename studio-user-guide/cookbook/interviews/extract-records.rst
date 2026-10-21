How to extract interview records data and dictionary?
=====================================================

The records of a study's interviews can be downloaded in a file from the study's **Data collection > Interviews** page.


Step 1 - Filter the records of interest
---------------------------------------

When the list of records is filtered, only the filtered records are downloaded. The list of records can be filtered by:

* Interview design, by selecting the interview design in the select box,
* Campaign, by selecting the campaign in the select box,
* State, by selecting the interview state in the select box,
* Eligibility, by selecting the associated participant eligibility in the select box,
* Capture time range, by entering From and/or To dates,
* Participant ID, by entering a string to match in the open text box.

Step 2 - Select the download format
-----------------------------------

The records can be downloaded in different formats.

**CSV**

The file downloaded is a text file in CSV format. There is no data dictionary included, only data (with one column per variable). The CSV file is divided in sections: one per form and its revision.

**CSV (zip)**

The file downloaded is a ZIP archive containing one folder per form-revision. Each of these folders includes:

* the data dictionary in a **variables.csv** file (in the format of Opal),
* the data in **data.csv** file. The CSV files header line are the variable names,
* the uploaded files, in a **files** folder.

**Excel**

The file downloaded is an Excel file, containing both the data dictionaries and the data. This Excel file contains several work sheets:

* **Variables** is a work sheet describing each variable for each form revision (identified by the **table** column),
* **Categories** is a work sheet describing each variable categories (i.e. select options),
* one work sheet for each form revision's collected data.

**JSON**

The file downloaded is a single JSON object dump. It is made of a data section with one entry per form-revision, each of these containing:

* the ``data`` array of collected data objects (one per interview),
* the ``variables`` array of variable objects (one per form field).

**Files**

The values of the file upload controls (see :ref:`cb_fe_files`) are exported as the path of each file, ``files/<id>/<file name>``, several paths for a control with several files. Only the **CSV (zip)** format includes the files themselves: each one is in the ``files`` folder next to the ``data.csv`` file of its form-revision, so that the paths of the data lead to them (this is also the structure expected by `Opal <https://www.obiba.org/pages/products/opal/>`_ for importing the files). With the other formats, the files can be downloaded one by one from the record page.

**Variables**

The form items are exported as variables of the following types:

* a number is ``integer`` when declared as such, ``decimal`` otherwise; a slider or a rating is ``integer``,
* a date is ``date``, a date-time is ``datetime``, a toggle is ``boolean``, a map location is a geometry (``point`` by default),
* a file upload is ``binary``, see the **Files** section above,
* a matrix (see :ref:`item_radio_matrix`) is split into one variable per row, named ``<matrix>.<row>``: the columns are the categories of a radio matrix, while each row of a checkbox matrix is a ``boolean`` (``false`` when the matrix was answered and the row was not checked),
* the variables of a repeatable group have one value per occurrence (a value sequence).

**From Opal**

`Opal <https://www.obiba.org/pages/products/opal/>`_ can import the records directly from Amber, using an API key (see :ref:`api_keys`).
