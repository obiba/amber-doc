How to extract records data and dictionary?
-------------------------------------------

The records of a study's case reports can be downloaded in a file from the study's Records page.


Step 1 - Filter the records of interest
---------------------------------------

When the list of records is filtered, only the filtered records are downloaded. The list of records can be filtered by:

* Form, by selecting the form in the select box,
* Patient ID, by entering a string to match in the open text box.

Step 2 - Select the download format
-----------------------------------

The download formats proposed in different formats.

**CSV**

The file downloaded is a ZIP archive containing one folder per form-revision. Each of these folders includes:

* the data dictionary in a **variables.json** file,
* the data in **data.csv** file. The CSV files header line are the variable names.

**JSON**

The file downloaded is a single JSON object dump. It is made of one entry per form-revision, each of these containg:

* the ``data`` array of collected data objects (one per case report),
* the ``variables`` array of variable objects (one per form field).
