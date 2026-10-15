.. _itws:

Interviews
==========

An **Interview design** describes a sequence of forms (the **steps**) that a participant has to fill, either by themselves (self-administered) or with the help of an interviewer, using the :doc:`Amber Visit <../../visit-user-guide/index>` app. The interview design is used by **Campaigns**, which group the **Participants** that are invited to do the interview. Each participant's answers are saved as an **Interview** record.

The interview data model is the following:

* A **Study** has **Interview designs**,
* An **Interview design** has ordered **Steps**, each step being linked to a **Form** (and optionally a **Form version**),
* An **Interview design** has **Campaigns**, each campaign having **Participants**,
* An **Interview** is the record of the data captured by a participant, one data entry per step.

Interview designs are listed in the study's **Design > Interview designs** page (left drawer). Selecting one opens the interview design page, organized in tabs: steps, campaigns, participants and translations.

Interview designs
-----------------

An interview design is defined by:

* A **Name**, unique in the study,
* A **Title** and a **Description**, displayed in the Amber Visit app,
* Some **Interviewer instructions** and **Participant instructions**, displayed in the Amber Visit app at the first visit, depending on who is conducting the interview,
* The access permissions: when **Restricted access** is enabled, only the **Permitted users** and/or **Permitted groups** can use it as interviewers,
* The state: **Paused** or **Active**.

From the list of interview designs, the following operations are available:

* **Add** an interview design,
* **Edit** the name, title, description, instructions and permissions,
* **Start** (activate) or **Pause** an interview design. An interview design is always created in the **Paused** state: participants cannot log in to it ("Interview is not active") and no campaign notifications are sent. Click on the play button to activate it,
* **Delete** one or more interview designs. Note that deleting an interview design also deletes its campaigns and their participants.

.. note::

  The translations of the interview design's and steps' texts (title, description, instructions) are looked up in the interview design's **Translations** tab. Translations can be exported and imported.

Steps
-----

The steps tab lists the forms that make the interview. Steps can be added, edited, moved up/down (the order of the steps is the order in which they are proposed to the participant) and deleted.

A step is defined by:

* A **Name**, unique in the interview design. The name ``participant`` is reserved,
* The **Form** and its **Form revision**. When no revision is specified, the latest revision of the form is used (not recommended in production, see :ref:`cb_designs`),
* A **Title** and a **Description**, displayed in the Amber Visit app,
* A **Time estimate** (min/average and max, in minutes), to inform the participant about the expected duration of the step,
* A **Condition** script: the visibility condition. When the condition is not satisfied, the step is removed from the interview,
* A **Disable** script: when the result is true, the step is visible but cannot be started (it is "waiting").

Condition and disable scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These scripts are JavaScript expressions that are evaluated in the Amber Visit app. A script can be either a value or a function that receives the ``data`` object. Variables can be referenced with the ``$('...')`` notation:

* ``$('participant.<attribute>')`` refers to a participant's attribute (see `Participants`_),
* ``$('<step name>.<field name>')`` refers to a field of a previous step. Only the data of the **completed** steps are available, the data of a step not yet started or in progress are empty.

Examples:

.. code-block:: javascript

  // visible only for adult participants
  $('participant.age') >= 18

  // visible only if a field of the step named 'screening' has a specific value
  $('screening.SMOKER') === 'yes'

  // disabled (waiting) until the step named 'consent' is completed
  !$('consent.AGREE')

.. note::

  If a script fails to evaluate, the step is considered visible (condition) and enabled (disable). When a step becomes hidden, its data are cleared.

Campaigns
---------

A campaign is a data collection period for an interview design, with its own set of participants and its own notification schedule. A campaign is defined by:

* A **Name**, unique in the interview design, and a **Description**,
* The **Investigators** (at least one) and the **Supporters**: these users can conduct the interviews of the campaign in Amber Visit, investigators also receive the campaign's notification emails,
* The validity period (**Valid from** and **Valid until** dates): participants cannot log in outside of this period,
* The notification schedule (see below),
* Whether participants must set a personal **password** (in addition to their participant code) at their first visit,
* Whether **walk-in** participants are accepted: a walk-in URL is then provided, which creates a new participant each time it is visited. Some default participant attributes can be set for the walk-in participants,
* The **Visit URL** (the Amber Visit app address, if different from the server's default one) and an optional **Completion URL**, to which the participant is redirected after the interview is completed,
* Whether investigators are notified when an interview is completed.

Notifications
~~~~~~~~~~~~~

The campaign's background tasks send emails to the **investigators** (not to the participants): it is the investigators' responsibility to contact the participants, using the participant codes and visit URLs listed in the CSV files attached to these emails. The schedule is based on the following campaign settings (default values in parentheses):

* **Weeks info before activation** (2): investigators are informed of participants that will be activated soon,
* At activation, investigators receive the list of newly activated participants (code, identifier, visit URL and attributes) to be contacted,
* **Weeks between reminders** (2) and **Number of reminders** (2): investigators receive the list of participants that have not completed their interview,
* **Weeks to deactivate** (18) and **Weeks info before deactivation** (3): investigators are informed of participants that will soon be deactivated; once the delay since activation has passed, participants are deactivated,
* A summary of the completed, in-progress and not-started interviews.

These tasks are only processed for active interview designs and campaigns within their validity period. They can also be triggered manually from the **Send notifications** menu of the campaigns list.

Participants
------------

A participant is defined by:

* A **Code**: a 6 characters code, generated by Amber, that the participant uses to log in Amber Visit,
* An optional **Identifier**: the study's own participant identifier,
* An optional validity period (**Valid from** and **Valid until** dates),
* Some **attributes** (key/value pairs), that can be used in the steps' condition scripts (``$('participant.<key>')``) and that are included in the extracted interview records,
* The activation state. A participant is **eligible** when activated and within its validity period. Note that a participant is automatically deactivated once its interview is completed.

From the list of participants, the following operations are available:

* **Add** a single participant (with identifier, validity dates and attributes), or several participants at once (by specifying a number of participants, without identifier),
* **Import** participants from a CSV file (comma, semicolon or tab separated, with a header line). The ``identifier``, ``validFrom``, ``validUntil`` and ``activated`` columns are recognized, all other columns are considered as participant attributes. The ``code`` column is ignored: codes are always generated by Amber,
* **Export** participants in CSV, Excel or JSON formats,
* **Activate**/**Pause**, view, edit, reset password or delete a participant.

Interview records
-----------------

The interviews are listed in the study's **Data collection > Interviews** page (left drawer). An interview is in one of the following states:

* **Initiated**: the participant has logged in but has not started any step,
* **In progress**: at least one step has been started,
* **Completed**: all the visible steps are completed.

The list can be filtered by interview design, campaign, state, eligibility, participant code and dates. From the list, an interview can be viewed (data in JSON format), its filling date can be edited, it can be deleted or **reopened**: reopening a completed interview reactivates the participant and sets all the steps back to "in progress", so that they can be amended.

The interview records can be exported in CSV, CSV (zip), Excel or JSON formats, see :doc:`../cookbook/interviews/extract-records`.

.. seealso::

  :ref:`cb_designs`
