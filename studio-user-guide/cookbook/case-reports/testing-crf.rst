How to test a case report form?
===============================

After a form has been designed, it is time to test it in the real world, without interfering with the normal data collection flow. We will use the following Amber's case report form (CRF) features:

* A CRF can be linked to a specific form version,
* Permission to use the CRF can be explicitly granted to some users or group of users.

Step 1 - Tag a new version of the form
--------------------------------------

After the design of the form is completed, with basic testing in the form builder preview, a new version of the form needs to be tagged. In the form builder page, select the **Tag** button and enter a comment describing what changes have been made.

You can verify that a new version has been added to the list of form revisions.

Step 2 - Create a CRF for this form version with restricted access
------------------------------------------------------------------

To create a new CRF, select the **Case Report Forms** menu in the left drawer and press the button to add a new CRF. The dialog that appears allows you to:

* Select the **Form** name to be tested,
* Select the **Revision** number that you just created,
* Select the **Restricted access** toggle button to open permissions options,
* Select the **Permitted users** and/or **Permitted groups** who will be allowed to use this CRF,
* Click on **Add**.

Step 3 - Start the CRF
----------------------

A CRF is always created in the **Paused** state. Because of this state, the CRF is not visible by the Amber Collect app. Click on the play icon to switch it to the **Active** state. Your CRF is now operational and only permitted users can see it.

Step 4 - Test in Amber Collect
------------------------------

Login in the Amber Collect web app. In the home page, the CRF should appear in the list (verify the version number displayed is the one you expect). Press on **Start** to collect new Case Report data with this CRF. Test different data entries to make sure conditions and validations are correct.

You do not necessarily need to save the Case Report to see what the data collected look like. After pausing the Case Report, select on the **Case Reports** menu (in the left drawer). The list of the Case Reports will appear. Click on the eye icon to see the data of this individual (in the standard `JSON <https://www.json.org>`_ format).

In case you have saved the Case Report data, the data cannot be seen in the Amber Collect any more. Then go to the Amber Studio app, select the study and the **Records** menu in the left drawer. Identify which case report you just saved (with the individual ID, form name and version) and press the eye icon to see the data (in JSON format). This test case report must then be removed to not pollute the real collected data.
