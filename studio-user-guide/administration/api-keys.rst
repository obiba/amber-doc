.. _api_keys:

API Keys
========

An API key allows an external application, such as `Opal <https://www.obiba.org/pages/products/opal/>`_, to extract the case reports and the interviews data, with their files, of some studies. A key is for data extraction only: it cannot modify anything.

With an API key, an application can:

* read the studies, the case report forms and the interview designs of the key's studies,
* export the case reports and the interviews of these studies (the same as a download from the records pages), and download their files,
* list the campaigns of these studies, to filter the interviews by campaign. Only the campaign names are disclosed, not their settings (investigators, reminders etc.).

The application sends the key in the ``x-api-key`` HTTP header of each request.

List of API keys
----------------

The list shows, for each key, the first characters of its value, its studies, its expiry date and when it was last used. The **Active** toggle (de)activates a key: an inactive or expired key is refused.

Add an API key
~~~~~~~~~~~~~~

When creating an API key, the following fields are available:

* **Name**, required, to identify the application using the key,
* **Description**, optional,
* **Studies**, required, the studies of which the data can be extracted,
* **Expires**, optional, the key is valid until the end of this day (in the time zone of the browser).

Once saved, the key value is shown **only once**: copy it then, Amber only stores a hash of it.

Edit an API key
~~~~~~~~~~~~~~~

The name, description, studies and expiry date can be modified at any time, the changes apply to the next requests.

Regenerate an API key
~~~~~~~~~~~~~~~~~~~~~

A new key value is generated (and shown once), the current one stops working immediately.

Delete an API key
~~~~~~~~~~~~~~~~~

The applications using the key lose access. When a study is deleted, it is also removed from the studies of the API keys.

View the audit
~~~~~~~~~~~~~~

The audit action of a key opens the :ref:`audit` page, filtered by this key.
