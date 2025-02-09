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

`Java <https://www.java.com>`_ is the minimum software requirement, other software are for a fully functional system. While Java is required by Opal server application, MongoDB, MySQL, R can be installed on another server. See also :doc:`rserver`.

======== ================= ==================================================================================================== ========================
Software Suggested version Download link                                                                                        Usage
======== ================= ==================================================================================================== ========================
Java     21                `OpenJDK downloads <https://jdk.java.net/>`_                                                         Java runtime environment
MySQL    >= 5.5.x          `MySQL downloads <http://www.mysql.com/downloads/mysql/>`_                                           Database engine
MongoDB  <= 6.0.x          `MongoDB Community downloads <https://www.mongodb.com/docs/v4.2/administration/install-community/>`_ Database engine
R        >= 4.x            `R downloads <http://cran.r-project.org/>`_                                                          Statistical analysis engine
======== ================= ==================================================================================================== ========================

Install
-------

Opal is distributed as a Debian/RPM package, as a zip file and as a Docker image. The resulting installation has default configuration that makes Opal ready to be used. Once installation is done, see :doc:`configuration` instructions.

Debian Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal is available as a Debian package from OBiBa Debian repository. To proceed installation, do as follows:

* `Install Debian package <http://www.obiba.org/pages/pkg/>`_. Follow the instructions in the repository main page for installing Opal.
* Manage Opal Service: after package installation, Opal server is running: see `Server launch`_.

RPM Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~

Opal is available as a RPM package from OBiBa RPM repository. To proceed installation, do as follows:

* `Install RPM package <http://www.obiba.org/pages/rpm/>`_. Follow the instructions in the RPM repository main page for installing Opal.
* Manage Opal Service: after package installation, Opal is running: see `Server launch`_.

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

Launch Opal. This step will create/update the database schema for Opal and will start Opal: see `Server launch`_.

For the administrator accounts, the credentials are "administrator" as username and "password" as password. See :ref:`user-dirs` to change it.

Docker Image Installation
~~~~~~~~~~~~~~~~~~~~~~~~~

OBiBa is an early adopter of the `Docker <https://www.docker.com/>`_ technology, providing its own images from the `Docker Hub repository <https://hub.docker.com/orgs/obiba/repositories>`_.

A typical `docker-compose <https://docs.docker.com/compose/>`_ file (including a MongoDB database and a MySQL database, a DataSHIELD ready R server and all useful plugins) would be:

.. code-block:: yaml

  version: '3'
  services:
    opal:
      image: obiba/opal:latest
      ports:
        - "8880:8080"
      depends_on:
        - rock
        - mongo
        - mysqldata
      environment:
        #- JAVA_OPTS=-Xms1G -Xmx8G -XX:+UseG1GC
        - OPAL_ADMINISTRATOR_PASSWORD=${OPAL_ADMINISTRATOR_PASSWORD}
        - MONGO_HOST=mongo
        - MONGO_PORT=27017
        - MYSQLDATA_HOST=mysqldata
        - MYSQLDATA_DATABASE=${MYSQLDATA_DATABASE}
        - MYSQLDATA_USER=${MYSQLDATA_USER}
        - MYSQLDATA_PASSWORD=${MYSQLDATA_PASSWORD}
        - ROCK_HOSTS=rock:8085
      volumes:
        - /some/path/opal:/srv
    mongo:
      image: mongo:6.0
    mysqldata:
      image: mysql
      environment:
        - MYSQL_DATABASE=${MYSQLDATA_DATABASE}
        - MYSQL_USER=${MYSQLDATA_USER}
        - MYSQL_PASSWORD=${MYSQLDATA_PASSWORD}
        - MYSQL_RANDOM_ROOT_PASSWORD=yes
    rock:
      image: obiba/rock:latest

The environment variables that are exposed by this image are:

=============================== =========================================================================
Environment Variable            Description
=============================== =========================================================================
``JAVA_OPTS``                   Java VM arguments.
``OPAL_ADMINISTRATOR_PASSWORD`` Opal administrator password, required and set at first start.
``APP_URL``                     Opal public URL (optional, see ``org.obiba.opal.public.url`` setting).
``APP_CONTEXT_PATH``            Opal server URL context (optional, see ``org.obiba.opal.server.context-path`` setting).
``MONGO_HOST``                  MongoDB server host (optional).
``MONGO_PORT``                  MongoDB server port, default is ``27017``.
``MONGO_USER``                  MongoDB server user (optional).
``MONGO_PASSWORD``              MongoDB server password (optional).
``MONGODATA_DATABASE``          MongoDB server data database name.
``MONGOIDS_DATABASE``           MongoDB server IDs database name (optional, ignored if a MySQL, MariaDB or PostgreSQL one is defined).
``MYSQLDATA_HOST``              MySQL server host for data storage (optional).
``MYSQLDATA_PORT``              MySQL server port.
``MYSQLDATA_DATABASE``          MySQL data database name.
``MYSQLDATA_USER``              MySQL data database user.
``MYSQLDATA_PASSWORD``          MySQL data database password.
``MYSQLIDS_HOST``               MySQL server host for IDs storage (optional).
``MYSQLIDS_PORT``               MySQL server port.
``MYSQLIDS_DATABASE``           MySQL IDs database name.
``MYSQLIDS_USER``               MySQL IDs database user.
``MYSQLIDS_PASSWORD``           MySQL IDs database password.
``MARIADBDATA_HOST``            MariaDB server host for data storage (optional).
``MARIADBDATA_DATABASE``        MariaDB data database name.
``MARIADBDATA_USER``            MariaDB data database user.
``MARIADBDATA_PASSWORD``        MariaDB data database password.
``MARIADBIDS_HOST``             MariaDB server host for IDs storage (optional, ignored if a MySQL one is defined).
``MARIADBIDS_DATABASE``         MariaDB IDs database name.
``MARIADBIDS_USER``             MariaDB IDs database user.
``MARIADBIDS_PASSWORD``         MariaDB IDs database password.
``POSTGRESDATA_HOST``           PostgreSQL server host for data storage (optional).
``POSTGRESDATA_DATABASE``       PostgreSQL data database name.
``POSTGRESDATA_USER``           PostgreSQL data database user.
``POSTGRESDATA_PASSWORD``       PostgreSQL data database password.
``POSTGRESIDS_HOST``            PostgreSQL server host for IDs storage (optional, ignored if a MySQL or MariaDB one is defined).
``POSTGRESIDS_DATABASE``        PostgreSQL IDs database name.
``POSTGRESIDS_USER``            PostgreSQL IDs database user.
``POSTGRESIDS_PASSWORD``        PostgreSQL IDs database password.
``AGATE_URL``                   Agate server URL (optional).
``AGATE_HOST``                  [Deprecated, use ``AGATE_URL``] Agate server host (optional).
``AGATE_PORT``                  [Deprecated, use ``AGATE_URL``] Agate server port, default is ``8444``.
``ROCK_HOSTS``                  Comma separated Rock R server URLs, for R server discovery (optional, but recommended).
``ROCK_ADMINISTRATOR_USER``     Default Rock server administrator user name (optional).
``ROCK_ADMINISTRATOR_PASSWORD`` Default Rock server administrator user password (optional).
``ROCK_MANAGER_USER``           Default Rock server manager user name (optional).
``ROCK_MANAGER_PASSWORD``       Default Rock server manager user password (optional).
``ROCK_USER_USER``              Default Rock server user user name (optional).
``ROCK_USER_PASSWORD``          Default Rock server user user password (optional).
``R_REPOS``                     R CRAN repositories (optional, see ``org.obiba.opal.r.repos`` setting).
=============================== =========================================================================

See also the `Rock R server Docker documentation <https://rockdoc.obiba.org/en/latest/admin/installation.html#docker-image-installation>`_.

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

  yum install opal-server

Zip Distribution Upgrade
~~~~~~~~~~~~~~~~~~~~~~~~

Follow the Installation of Opal Zip distribution above but make sure you don't overwrite your opal-home directory.

Docker Distribution Upgrade
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Change the docker image version and restart the docker container. If the opal-home directory was mounted in user space, it will be reused.

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

Execute the command line (bin directory is in your execution PATH)):

.. code-block:: bash

  opal

The Opal server log files are located in **OPAL_HOME/logs** directory. If the logs directory does not exist, it will be created by Opal.

**Docker**

When using a docker-compose configuration file, the start up command is:

.. code-block:: bash

  docker-compose -f docker-compose.yml up -d


Usage
~~~~~

To access Opal with a web browser the following urls may be used (port numbers may be different depending on HTTP Server Configuration):

* http://localhost:8080 will provide a connection without encryption,
* https://localhost:8443 will provide a connection secured with ssl.

Troubleshooting
~~~~~~~~~~~~~~~

If you encounter an issue during the installation and you can't resolve it, please report it in our `Opal Issue Tracker <https://github.com/obiba/opal/issues>`_.

Opal logs can be found in **/var/log/opal**. If the installation fails, always refer to this log when reporting an error.
