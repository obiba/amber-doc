Introduction
============

The Amber Collect application is the case report data collection web interface of the Amber server. The Case Report Forms that are enabled can be used to report cases.

Using Amber Collect requires authentication. Depending on the user role and authorizations, some Case Report Forms will be visible or not.

**No personal information is stored in the app** after the case report has been completed: private data are automatically saved on the Amber server (as soon as the network is accessible) and cannot be read back.

Requirements
------------

This web interface is a JavaScript application requiring a modern web browser. There is no requirement regarding the operating system: it can be either a desktop or a mobile one.

Installation
------------

Amber Collect is a `Progressive Web App <https://web.dev/what-are-pwas/>`_ which means that it is a web app (i.e. accessible from a browser) that can be installed on the user's desktop (computer) or home screen (mobile), without the need of deploying it in a proprietary App Store.

Step 1 - Go to Amber Collect web site
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In your favorite browser, enter the Amber Collect app address, e.g. `https://amber-collect-demo.obiba.org <https://amber-collect-demo.obiba.org>`_. From this point, the app is fully functional. The page can be bookmarked or "installed" (see next Step).

Step 2 - Install the app (optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Depending on the browser's vendor, the procedure to install a shortcut icon to your home screen might differ a bit.

.. grid:: 1 2 3 3

    .. grid-item::

        Chrome

        .. figure:: images/amber-collect-chrome-install.png
          :width: 200

          Install Amber Collect app from Chrome browser: a popup message proposes to install the app.

    .. grid-item::

        Firefox/Ghostery

        .. figure:: images/amber-collect-firefox-install.png
          :width: 200

          Install Amber Collect app from Firefox browser: the "Install" entry is proposed in the page's menu.


    .. grid-item::

        Phoenix

        .. figure:: images/amber-collect-phoenix-install.png
          :width: 200

          Install Amber Collect app from Phoenix browser: the "Add to home screen" action is proposed in the page's menu.

App updates
~~~~~~~~~~~

When a new version of Amber Collect is deployed, a **Updated content is available** message is displayed: press **Refresh** to reload the app with the new version.

Offline Usage
-------------

Once loaded, Amber Collect keeps working without network access:

* the case reports that are completed while offline are kept in the browser, and their saving to the Amber server is retried automatically every minute, until the network is accessible again;
* the files picked in the file upload controls of a form are stored in the browser, and uploaded when the case report is saved to the Amber server. They are then deleted from the browser. Deleting a case report that was not saved also deletes its files.

.. note::
  Do not clear the browser data of the app while some case reports are pending: they would be lost.
