.. _records:

Records
=======

Each record is a Case report and then contains:

* Which form was used to capture data, in which version,
* The captured data, identified by the patient ID,
* The user and the date at which the record was created,
* The list of actions that were performed on the case report.

An action on the case report contains the following information:

* The type of action: `init` when the interview is started, `pause` when it is paused and `complete` when it is finished,
* The user who performed the action,
* The timestamp at which the action was performed.

List of records
---------------

Delete record(s)
~~~~~~~~~~~~~~~~

To delete several records:

* Select one or more record in the list,
* Press the Delete selected records button and confirm.

You can also delete a specific record by pressing the record's Delete action button.

Filter records
~~~~~~~~~~~~~~

The list of records can be filtered by:

* Case report form (and therefore the associated form and its revisions used to collect data), by selecting the case report form in the select box,
* Form (any revisions), by selecting the form in the select box,
* Captured time range, by selecting the **From** and/or **To** dates,
* Patient ID, by entering a string to match in the open text box.

Download records
~~~~~~~~~~~~~~~~

For consistency, records are always grouped by their form-revision. The downloaded file will contain:

* The data in the selected format,
* The data dictionary, which is a translation of the form schema: each item (capturing data) is a variable (labels are included within the variable, options are the variable's categories etc.).

The download formats proposed are:

* CSV, downloaded as a text file in CSV format. There is one section per "Case report form". The header line of each section are the variable names.
* CSV (zip), downloaded as a ZIP archive containing: one folder per form-revision including the data dictionary in **variables.json** file and the data in **data.csv** file. The CSV files header line are the variable names.
* Excel, downloaded as an Excel file containing several work sheets: **Variables** are the variables for each of the "Case report form" (named by the **table** column), **Categories** are the variable categories and one sheet per "Case report form" holding the data in tabular format (one column per variable).
* JSON, downloaded as a single JSON object dump made of: one entry per form-revision, each of these containing the ``data`` array and the ``variables``.

Note also that:

* When the list of records is filtered, only the filtered records are downloaded,
* Each download is audited: who triggered the download, with which filter criteria, about which patients,
* The meta information about the record (user, history of actions) are not included in the downloaded file.

View record
~~~~~~~~~~~

View the captured raw data of a single record by pressing the Eye button.
