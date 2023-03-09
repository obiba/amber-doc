Installation
============

Amber is a system of three applications:

* **Amber** server: Business layer over the database: users, groups, studies, forms, case records etc. are all defined in this application and their access require authentication and authorization. It is only accessible via an API.
* **Amber Studio** web app: Content management web application, using data and services of the Amber server
* **Amber Collect** web app: Case report data collection web app, using data and services of the Amber server

These applications are written in JavaScript.

Requirements
------------

Server Hardware Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

============ ===============
Component    Requirement
============ ===============
CPU	         Recent server-grade or high-end consumer-grade processor
Disk space	 8GB or more.
Memory (RAM) Minimum: 4GB, Recommended: >4GB
============ ===============

Server Software Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Amber server and apps are pure Javascript software based on `nodejs <https://nodejs.org/>`_ (Amber) or `Quasar <https://quasar.dev/>`_ (Amber Studio and Amber Collect). Despite it could be possible to set up a native runtime environment, we recommend to use a containerized one (Docker), to facilitate to customization and the deployment of the software applications.

The database that is used by Amber server is `MongoDB <https://www.mongodb.com/>`_ which can also be deployed from a container.

========================= ================================================================ ========================
Software                  Documentation                                                    Usage
========================= ================================================================ ========================
Docker Engine             `Docker Engine <https://docs.docker.com/engine/>`_               Docker runtime environment
Docker Compose            `Docker Compose <https://docs.docker.com/compose/>`_             Docker compose plugin
========================= ================================================================ ========================

Install
-------

Docker Images Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~

Because the Amber system is composed of different parts (server and client applications), these need to be integrated with each other for the specific site where they will be deployed.

The set up of the different Docker images of Amber is described in the `amber-template project <https://github.com/obiba/amber-template>`_.

The steps to follow are:

1. Download or clone the ``amber-template`` repository,
2. Define the Amber (server and apps) parts (configuration and/or source files) to customize,
3. Use the ``Docker Compose`` tool to build and run these images in your specific environment.

The environment variables that are exposed by the ``amber`` image are:

=============================== =========================================================================
Environment Variable            Description
=============================== =========================================================================
``CLUSTER_COUNT``               Node cluster count, defaults to all available CPU cores
``APP_NAME``                    JWT issuer
``APP_SECRET_KEY``              Encryption key
``APP_SECRET_IV``               Secret string for the encryption's initial vector,
``APP_URL``                     JWT audience
``CLIENT_URLS``                 Comma separated client urls, for the CORS policy
``AMBER_STUDIO_URL``            Amber Studio app url, to be included in the notification emails
``AMBER_COLLECT_URL``           Amber Collect app url, to be included in the notification emails
``MONGODB_URL``                 The MongoDB connection string
``ENCRYPT_DATA``                Whether the patient/participant data should be encrypted in the database
``RECAPTCHA_SECRET_KEY``        The `reCAPTCHA v3 <https://developers.google.com/recaptcha/docs/v3>`_ secret key.
``GMAIL``                       The Gmail user name for the notification service (optional, only if Gmail transport service is used)
``GMAIL_PASSWORD``              The Gmail user password for the notification service (optional, only if Gmail transport service is used)
``SENDINBLUE_API_KEY``          The `Sendinblue <https://www.sendinblue.com/>`_ API key for the notification service (optional, only if Sendinblue transport service is used)
``SMTP_HOST``                   The SMTP server host
``SMTP_NAME``                   The SMTP server name
``SMTP_SECURE``                 Whether the SMTP connection should use SSL
``SMTP_REQUIRE_TLS``            Whether the SMTP connection should use TLS (when secure is false)
``SMTP_LOGGER``                 Enable SMTP logging
``SMTP_DEBUG``                  Enable SMTP debug by sending log events
``SMTP_USER``                   The SMTP server user
``SMTP_PASSWORD``               The SMTP server user's password
``FROM_EMAIL``                  The automated sender email address,
``ADMINISTRATOR_EMAIL``         User seeding when there is no administrator in the database
``ADMINISTRATOR_PWD``           User seeding when there is no administrator in the database
``LOG_LEVEL``                   Logger level (`error`` `warn`` `info`` `verbose`` `debug`` `silly`` etc. (see [winstonjs](https://github.com/winstonjs/winston))), default is `info`
``LOG_FILE``                    File logger path
``LOG_FILE_LEVEL``              File logger level when `LOG_FILE` is specified, default is `LOG_LEVEL`
``NODE_ENV``                    Name of the config file to be merged with the default one (e.g. `production`)
=============================== =========================================================================

The environment variables that are exposed by the ``amber-studio`` and ``amber-collect`` images are:

=============================== =========================================================================
Environment Variable            Description
=============================== =========================================================================
``AMBER_URL``                   The URL to the Amber server.
``RECAPTCHA_SITE_KEY``          The `reCAPTCHA v3 <https://developers.google.com/recaptcha/docs/v3>`_ site key.
=============================== =========================================================================

Upgrade
-------

The upgrade procedures are handled by the application itself.

Usage
~~~~~

To access Amber with a web browser the following urls may be used (port numbers may be different depending on Docker Compose configuration):

* Amber Server: http://localhost:3030/
* Amber Studio: http://localhost:3080/
* Amber Collect: http://localhost:3090/

Troubleshooting
~~~~~~~~~~~~~~~

If you encounter an issue during the installation and you can't resolve it, please report it in our `Amber Issue Tracker <https://github.com/obiba/amber/issues>`_.
