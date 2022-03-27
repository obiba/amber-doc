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

* Form, by selecting the form in the select box,
* Patient ID, by entering a string to match in the open text box.

Download records
~~~~~~~~~~~~~~~~

For consistency, records are always grouped by their form-revision. The downloaded file will contain:

* The data in the selected format,
* The data dictionary, which is a translation of the form schema: each item (capturing data) is a variable (labels are included within the variable, options are the variable's categories etc.).

The download formats proposed are:

* CSV, downloaded as a ZIP archive containg: one folder per form-revision including the data dictionary in **variables.json** file and the data in **data.csv** file. The CSV files header line are the variable names.
* JSON, downloaded as a single JSON object dump made of: one entry per form-revision, each of these containg the ``data`` array and the ``variables``.

Note also that:

* When the list of records is filtered, only the filtered records are downloaded,
* Each download is audited: who triggered the download, whith which filter criteria, about which patients,
* The meta information about the record (user, history of actions) are not included in the downloaded file. 

View record
~~~~~~~~~~~

View the captured raw data of a single record by pressing the Eye button.
