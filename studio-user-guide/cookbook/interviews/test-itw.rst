.. _cb_designs:

How to test an interview design?
================================

After some forms have been designed, it is time to test them in the real world, without interfering with the normal data collection flow. We will use the following Amber's interview design features:

* Each step of an interview design can be linked to a specific form version,
* Permission to use the interview design can be explicitly granted to some users or a group of users.

Step 1 - Tag a new version for each form
----------------------------------------

After the design of a form is completed, with basic testing in the form builder preview, a new version of the form needs to be tagged. In the form builder page, select the **Tag** button and enter a comment describing what changes have been made.

You can verify that a new version has been added to the list of form revisions.

Step 2 - Create an interview design with restricted access
----------------------------------------------------------

To create a new interview design, select the **Design > Interview designs** menu in the left drawer and press the button to add a new interview design. The dialog that appears allows you to:

* Enter a name and a title for this design,
* Select the **Restricted access** toggle button to open permissions options,
* Select the **Permitted users** and/or **Permitted groups** who will be allowed to use this design,
* Click on **Add**.

Then in this interview design page, add for each interview step:

* Select the **Form** name to be tested,
* Select the **Revision** number that you just created.

Add a test campaign with participants. When adding participants, make sure they have any attributes that could be interpreted by the form's logical rules.

Step 3 - Start the interview design
-----------------------------------

An interview design is always created in the **Paused** state. Because of this state, no participant could be identified by the Amber Visit app. Click on the play icon to switch it to the **Active** state. Your interview design is now operational and only permitted users can see it.

Step 4 - Test in Amber Visit
----------------------------

As one of the participant, login in the Amber Visit web app. In the home page, the interview steps should appear. Start answering interview steps and test different data entries to make sure conditions and validations within each form and between steps are correct.

Once the interview is saved, go to the Amber Studio app, select the study and the **Data collection > Interviews** menu in the left drawer. Identify which interview you just saved (with the participant ID) and press the eye icon to see the data (in JSON format). This test interview must then be removed to not pollute the real collected data.
