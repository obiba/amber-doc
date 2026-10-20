Introduction
============

The Amber Visit application is the interview data collection web interface of the Amber server. The Interview Designs that are enabled can be used to conduct interviews, either self-administered by the participant or with the help of a dedicated interviewer.

Using Amber Visit requires authentication. A participant will provide its personal code (and optionally a password), an interviewer will use its Amber credentials (user name, password and 2FA code).

**No personal information is stored in the app** after the interview has been completed: private data are automatically saved on the Amber server (as soon as the network is accessible).

Requirements
------------

This web interface is a JavaScript application requiring a modern web browser. There is no requirement regarding the operating system: it can be either a desktop or a mobile one.

Installation
------------

Amber Visit is a `Progressive Web App <https://web.dev/what-are-pwas/>`_: it is accessible from a browser, at the Amber Visit app address, and it can also be installed on the user's desktop (computer) or home screen (mobile), the same way as Amber Collect (see the Amber Collect installation steps). Once loaded, the app keeps working when the network is temporarily not accessible (see `Offline data`_).

When a new version of Amber Visit is deployed, a **Updated content is available** message is displayed: press **Refresh** to reload the app with the new version.

Prerequisites
-------------

Before an interview can be conducted, the following must be set up in Amber Studio (see :ref:`itws`):

* An **Interview design** with its steps, in the **Active** state,
* A **Campaign** within its validity period,
* Some **Participants** in this campaign, each with a participant code (unless walk-in participants are accepted).

Login
-----

As a participant
~~~~~~~~~~~~~~~~

The participant enters the 6 characters participant code given by an investigator. If the campaign requires a password, the participant creates a personal password at the first connection (8 characters minimum), and must provide it at each subsequent connection. A forgotten password can be reset by an investigator from Amber Studio.

The participant can also follow a direct link that includes the code, of the form ``https://<amber-visit-address>/go/<code>``. Such links are listed in the CSV files attached to the campaign's notification emails.

If the campaign accepts walk-in participants, visiting the campaign's walk-in URL creates a new participant and starts its interview immediately.

The login is refused if the participant is not eligible: deactivated (for instance because the interview is already completed), outside of the participant's or the campaign's validity period, or if the interview design is paused.

As an interviewer
~~~~~~~~~~~~~~~~~

Select **I am an investigator** and log in with your Amber credentials (email and password, then the 2FA code). Then enter the **Participant code** and press **Start**. Only the investigators and supporters of the participant's campaign are allowed to conduct its interview.

Conducting the interview
------------------------

The home page displays the interview design's title, description and instructions (participant or interviewer instructions), followed by the list of the steps. Only the steps whose condition is satisfied are listed (see :ref:`itws`). Each step shows an action depending on its state:

* **Start**: the step has not been started yet,
* **Continue**: the step was started and paused,
* **Waiting**: the step cannot be started yet (its disable condition applies, for instance because it depends on a step that is not completed),
* **Completed**: the step data have been saved.

In a step, the form is filled page by page (**Previous**/**Next**) or in a single page (with a **Go to...** table of contents), depending on the form's settings. At any time, **Pause** saves the step's data and goes back to the home page: the step can be continued later, including after logging out. **Validate and save** (or **Finish**) validates the form and completes the step. A completed step cannot be modified anymore.

The interview is completed when all the listed steps are completed. The participant is then deactivated and cannot log in anymore. If a **Completion URL** is defined in the campaign, the participant is redirected to it. When conducted by an interviewer, the interview's **Filling date** can be adjusted after completion.

.. note::

  A completed interview can be reopened from Amber Studio (**Data collection > Interviews**), if some answers need to be amended.

Files
~~~~~

Some forms ask for files (pictures, scans, documents...) with file upload controls. The picked files are stored in the browser, and uploaded to the Amber server when the step is saved (on **Pause** or on completion). The uploaded files can then be downloaded by the investigators from Amber Studio.

Language
~~~~~~~~

The language can be selected from the app's menu. The forms are displayed in the languages for which the interview design has translations.

Offline data
~~~~~~~~~~~~

If the network is not accessible when the step data are saved, the step data (and its files) are kept in the browser and a **Pending data save (are you offline?)** banner is displayed. The pending steps are saved automatically when the network is back, and retried every minute; press **Save now** to send the pending data to the Amber server immediately.

.. note::
  Do not clear the browser data of the app, nor log out, while some steps are pending: they would be lost.
