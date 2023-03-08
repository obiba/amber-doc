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
