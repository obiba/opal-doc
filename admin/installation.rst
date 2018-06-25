Installation
============

Opal is a stand-alone `Java <https://www.java.com>`_ server application that does not require a database engine at installation time. Connection to one or more databases is part of the post-install configuration.

Requirements
------------

Server Hardware Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

============ ===============
Component    Requirement
============ ===============
CPU	         Recent server-grade or high-end consumer-grade processor
Disk space	 8GB or more (data are stored within the database, not in Opal server space).
Memory (RAM) Minimum: 4GB, Recommended: >8GB
============ ===============

Server Software Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Java <https://www.java.com>`_ is the minimum software requirement, other software are for a fully functional system.

======== ================= ========================================================== ========================
Software Suggested version Download link                                              Usage
======== ================= ========================================================== ========================
Java     >= 1.8.x          `Java Oracle downloads <https://www.java.com>`_            Java runtime environment
MySQL    >= 5.5.x          `MySQL downloads <http://www.mysql.com/downloads/mysql/>`_ Database engine
MongoDB  >= 2.4.x          `MongoDB downloads <http://www.mongodb.org/downloads>`_    Database engine
R        >= 3.0.x          `R downloads <http://cran.r-project.org/>`_                Statistical analysis engine
======== ================= ========================================================== ========================

While Java is required by Opal server application, MongoDB/MySQL/R can be installed on another server.

Install
-------

Opal is distributed as a Debian/RPM package and as a zip file. The resulting installation has default configuration that makes Opal ready to be used. Once installation is done, see :doc:`configuration` instructions.

Debian Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal is available as a Debian package from OBiBa Debian repository. To proceed installation, do as follows:

* `Install Debian package <http://www.obiba.org/pages/pkg/>`_. Follow the instructions in the repository main page for installing Opal.
* Manage Opal Service: after package installation, Opal server is running: see how to manage the Service.

RPM Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~

Opal is available as a RPM package from OBiBa RPM repository. To proceed installation, do as follows:

* `Install RPM package <http://www.obiba.org/pages/rpm/>`_. Follow the instructions in the RPM repository main page for installing Opal.
* Manage Opal Service: after package installation, Opal is running: see how to manage the Service.

Zip Distribution Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal is also available as a Zip file. To install Opal zip distribution, proceed as follows:

* `Download Opal distribution <https://github.com/obiba/opal/releases>`_
* Unzip the Opal distribution. Note that the zip file contains a root directory named **opal-x.y.z-dist** (where x, y and z are the major, minor and micro releases, respectively). You can copy it wherever you want. You can also rename it.
* Create an ``OPAL_HOME`` environment variable
* Separate Opal home from Opal distribution directories (recommended). This will facilitate subsequent upgrades.

Set-up example for Linux:

.. code-block:: bash

  mkdir opal-home
  cp -r opal-x-dist/conf opal-home
  export OPAL_HOME=`pwd`/opal-home
  ./opal-x-dist/bin/opal

Launch Opal. This step will create/update the database schema for Opal and will start Opal: see Regular Command.

For the administrator accounts, the credentials are "administrator" as username and "password" as password. See User Directories Configuration to change it.

Upgrade
-------

The upgrade procedures are handled by the application itself.

Debian Package Upgrade
~~~~~~~~~~~~~~~~~~~~~~

If you installed Opal via the Debian package, you may update it using the command:

.. code-block:: bash

  apt-get install opal

RPM Package Upgrade
~~~~~~~~~~~~~~~~~~~

If you installed Opal via the RPM package, you may update it using the command:

.. code-block:: bash

  yum install opal

Zip Distribution Upgrade
~~~~~~~~~~~~~~~~~~~~~~~~

Follow the Installation of Opal Zip distribution above but make sure you don't overwrite your opal-home directory.

Execution
---------

Server launch
~~~~~~~~~~~~~

**Service**

When Opal is installed through a Debian/RPM package, Opal server can be managed as a service.

Options for the Java Virtual Machine can be modified if Opal service needs more memory. To do this, modify the value of the environment variable ``JAVA_ARGS`` in the file **/etc/default/opal**.

Main actions on Opal service are: ``start``, ``stop``, ``status``, ``restart``. For more information about available actions on Opal service, type:

.. code-block:: bash

  service opal help

The Opal service log files are located in **/var/log/opal** directory.

**Manually**

The Opal server can be launched from the command line. The environment variable ``OPAL_HOME`` needs to be setup before launching Opal manually.

==================== ======== ===========
Environment variable Required Description
==================== ======== ===========
``OPAL_HOME``        yes      Path to the Opal "home" directory.
``JAVA_OPTS``        no       Options for the Java Virtual Machine. For example: `-Xmx4096m -XX:MaxPermSize=256m`
==================== ======== ===========

To change the defaults update:  ``bin/opal`` or ``bin/opal.bat``

Make sure Command Environment is setup and execute the command line (bin directory is in your execution PATH)):

.. code-block:: bash

  opal

Executing this command upgrades the Opal server and then launches it.

The Opal server log files are located in **OPAL_HOME/logs** directory. If the logs directory does not exist, it will be created by Opal.

Usage
~~~~~

To access Opal with a web browser the following urls may be used (port numbers may be different depending on HTTP Server Configuration):

* http://localhost:8080 will provide a connection without encryption,
* https://localhost:8443 will provide a connection secured with ssl.

Troubleshooting
~~~~~~~~~~~~~~~

If you encounter an issue during the installation and you can't resolve it, please report it in our `Opal Issue Tracker <https://github.com/obiba/opal/issues>`_.

Opal logs can be found in **/var/log/opal**. If the installation fails, always refer to this log when reporting an error.
