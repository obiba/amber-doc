Installation
============

Amber is a system of three applications:
* Amber server: Business layer over the database: users, groups, studies, forms, case records etc. are all defined in this application and their access require authentication and authorization. It is only accessible via an API.
* Amber Studio web app: Content management web application, using data and services of the Amber server
* Amber Collect web app: Case report data collection web app, using data and services of the Amber server

These applications are written in javascript

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

======== ================= ================================================================ ========================
Software Suggested version Download link                                                    Usage
======== ================= ================================================================ ========================
Nodejs   16.x              `Nodejs <https://nodejs.org/>`_                                  Javascript runtime environment
MongoDB  >= 5.x            `MongoDB downloads <https://www.mongodb.com/>`_                  Database engine
======== ================= ================================================================ ========================

While Nodejs is required by the Amber server application, MongoDB can be installed on another server.

Install
-------

Docker Image Installation
~~~~~~~~~~~~~~~~~~~~~~~~~

OBiBa is an early adopter of the `Docker <https://www.docker.com/>`_ technology, providing its own images from the `Docker Hub repository <https://hub.docker.com/orgs/obiba/repositories>`_.

A typical `docker-compose <https://docs.docker.com/compose/>`_ file (including a MongoDB database) would be:

.. code-block:: yaml

  version: '3'
  services:
          amber:
                  build: ${TARGET}/amber
                  ports:
                          - "3320:3030"
                  links:
                          - mongo
                  environment:
                          - CLIENT_URLS=*
                          - MONGODB_URL=mongodb://mongo:27017/amber
                          - ADMINISTRATOR_EMAIL=${ADMINISTRATOR_EMAIL}
                          - ADMINISTRATOR_PWD=${ADMINISTRATOR_PWD}
                          - AMBER_STUDIO_URL=${AMBER_STUDIO_URL}
                          - RECAPTCHA_SECRET_KEY=${RECAPTCHA_SECRET_KEY}
                          - GMAIL=${GMAIL}
                          - GMAIL_PASSWORD=${GMAIL_PASSWORD}
          mongo:
                  image: mongo
          amber-studio:
                  build:
                          context: ${TARGET}/amber-studio
                          args:
                                  - AMBER_URL=${AMBER_URL}
                                  - RECAPTCHA_SITE_KEY=${RECAPTCHA_SITE_KEY}
                  ports:
                          - "3380:80"
          amber-collect:
                  build:
                          context: ${TARGET}/amber-collect
                          args:
                                  - AMBER_URL=${AMBER_URL}
                  ports:
                          - "3390:80"

Then environment variables that are exposed by this image are:

================================= =========================================================================
Environment Variable              Description
================================= =========================================================================
``.``                             .
================================= =========================================================================

Upgrade
-------

The upgrade procedures are handled by the application itself.

Usage
~~~~~

To access Amber with a web browser the following urls may be used (port numbers may be different depending on HTTP Server Configuration):

* http://localhost:3030/ will provide a basic html showing the server is up and running.

Troubleshooting
~~~~~~~~~~~~~~~

If you encounter an issue during the installation and you can't resolve it, please report it in our `Amber Issue Tracker <https://github.com/obiba/amber/issues>`_.
