.. _crfs:

Case Report Forms
=================

The Case report forms drives the way the form will be used by the interviewers. It defines:

* The version of the form to be used,
* The access permissions,
* The activity (enabled/disabled).

.. note::

  For now Amber supports only patients data acquisition via an interviewer. In the future versions, it could be possible to capture data about a predefined list of participants (with some selection criteria) or do some self-reporting. The case report form activity could also be scheduled. Please contact us if you have more complex use-cases.


List of case report forms
-------------------------

From the list of case report forms the following operations are available:

Add a case report form
~~~~~~~~~~~~~~~~~~~~~~

Adding a case report form requires to select a form (in the current study) and its revision. If no revision is defined for the selected form, a new revision will be created. The revision number can be explicitly specified or the ``latest`` can be used (not recommended, see :ref:`cb_testing_crf`).

By default a Case report form can be used by all the interviewers. It is possible to restrict the access to the selected users and/or groups.

Delete case report form(s)
~~~~~~~~~~~~~~~~~~~~~~~~~~

To delete several case report forms:

* Select one or more case report forms in the list,
* Press the Delete selected case report forms button and confirm.

You can also delete a specific case report form by pressing the case report form's Delete action button.

Edit a case report form
~~~~~~~~~~~~~~~~~~~~~~~

A case report form can be edited: only the revision number and/or the access permissions can be amended. To change the form, create a new case report form.

Pause/start a case report form
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After being created, a case report form is in `Paused` state: it is not visible by the interviewers. Click on the Play button to activate the case report form. A case report form can be paused at any time: any pending case reports will be rejected at submission time.
