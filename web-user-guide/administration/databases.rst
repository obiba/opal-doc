Databases
=========

The databases administration page allows to manage the server databases. A fully operational Opal server requires to have at least two different databases registered for:

* identifiers mapping storage (one and only one required, see :doc:`../../ids` section for more details)
* data storage (at least one is required)

Additional databases can be declared for other usages: data import, data export.

Opal currently supports two different type of database engines:

* SQL database (`MySQL <https://www.mysql.com/>`_, `MariaDB <https://mariadb.org/>`_, `PostgreSQL <https://mariadb.org/>`_) for storage, import, export,
* Document database (`MongoDB <https://www.mongodb.org/>`_) for storage only.

The following table summarizes the different database usages depending on the database engine and the schema used to store the data.

=========================== =============== ======= ======= =======
Database Engine             Data Schema     Storage Import  Export
=========================== =============== ======= ======= =======
MySQL, MariaDB              Opal SQL        x
MySQL, MariaDB, PostgreSQL  Tabular SQL     x       x       x
MySQL, MariaDB, PostgreSQL  Limesurvey              x
MongoDB                     Opal Documents  x
=========================== =============== ======= ======= =======

Database Engines
----------------

SQL Databases
~~~~~~~~~~~~~

Currently the supported SQL database engines are: MySQL, MariaDB and PostgreSQL. Make sure the corresponding database users are granted all privileges on their respective database instances (CREATE TABLE, ALTER, and so on).

MySQL
^^^^^

At the time of writing this document, at least MySQL 5.5.x is recommended.

**MySQL Server Configuration**

Edit the my.cnf file (often named my.ini on Windows operating systems) in your MySQL server. Locate the [mysqld] section in the file, and add or modify the following parameters:

* specify the default character set to be UTF-8:

.. code-block:: text

  [mysqld]
  character-set-server=utf8
  collation-server=utf8_bin

* set the default storage engine to InnoDB:


.. code-block:: text

  [mysqld]
  default-storage-engine=INNODB

* if you plan to store binary data into Opal, configure the packet size that wil be transmitted to or from MySQL. See `Packet Too Large <http://dev.mysql.com/doc/refman/5.5/en/packet-too-large.html>`_ documentation.


.. code-block:: text

  [mysqld]
  max_allowed_packet=1G

* we also recommend to use Per-Table Tablespaces. See `InnoDB File-Per-Table Tablespaces <http://dev.mysql.com/doc/refman/5.5/en/innodb-multiple-tablespaces.html>`_ documentation.


.. code-block:: text

  [mysqld]
  innodb_file_per_table

**MySQL Database Creation**

When creating the MySQL database that Opal should connect to, make sure the character set is specified as UTF-8 with binary UTF-8 collation (for case-sensitive collation).


.. code-block:: sql

  CREATE DATABASE opal CHARACTER SET utf8 COLLATE utf8_bin;

The `default MySQL storage engine must also be InnoDB <http://dev.mysql.com/doc/refman/5.5/en/innodb-default-se.html>`_.

Sample script for MySQL database creation:

.. code-block:: sql

  # Create Opal database and user.
  #
  # Command: mysql -u root -p < create_opal_database.sql
  #

  CREATE DATABASE opal_data CHARACTER SET utf8 COLLATE utf8_bin;

  CREATE USER 'opal' IDENTIFIED BY '<opal-user-password>';
  GRANT ALL ON opal_data.* TO 'opal'@'localhost' IDENTIFIED BY '<opal-user-password>';
  FLUSH PRIVILEGES;

PostgreSQL
^^^^^^^^^^

PostgreSQL is currently supported for all usages associated with the Tabular SQL schema (import/export and storage). Limitations associated with this type of schema applies.

Document Databases
~~~~~~~~~~~~~~~~~~

Currently the only No-SQL engine that is supported is the document oriented database MongoDB.

MongoDB
^^^^^^^

MongoDB does not require the database to exist before you access it. So you could just install MongoDB and configure your database in Opal.

It is however recommended that you restrict access to your MongoDB database, to achieve this you need to:

* create a user with the proper roles on the target databases
* run the MongoDB service with `Client Access Control <http://docs.mongodb.org/manual/tutorial/enable-authentication/>`_ enabled. Once the MongoDB service runs with Client Access Control enabled, all database connections must be authenticated.
* specify the authentication source database in the connection URL. Example of connection URLs: ``mongodb://localhost:27017/opal_ids?authSource=admin``, ``mongodb://localhost:27017/opal_data?authSource=admin``

The example below creates the opaladmin user for opal_ids and opal_data databases:

.. code-block:: javascript

  use admin
  db.createUser(
    {
      user: "opaladmin",
      pwd: "opaladmin",
      roles: [
        {
          "role" : "readWrite",
          "db" : "opal_ids"
        },
        {
          "role" : "dbAdmin",
          "db" : "opal_ids"
        },
        {
          "role" : "readWrite",
          "db" : "opal_data"
        },
        {
          "role" : "dbAdmin",
          "db" : "opal_data"
        },
        {
            "role": "clusterMonitor",
            "db": "admin"
        },
        {
            "role": "readAnyDatabase",
            "db": "admin"
        }
      ]
    }
  )

Opal requires either *clusterMonitor* or *readAnyDatabase* role on the *admin* database for validation operations. The first role is useful for a cluster setup and the latter if your MongoDB is on a single server.

Opal supports connection to `MongoDB using SSL <https://docs.mongodb.com/manual/tutorial/configure-ssl/>`_: add the ``ssl=true`` (and any other relevant parameters) to the `MongoDB connection string <https://docs.mongodb.com/manual/reference/connection-string/>`_. The system key-pair (see :ref:`encryption-keys`) will be used for connecting to the database. If the MongoDB server certificate is self-signed, its certificate can be added to the Opal trusted certificates store by creating a Opal user authenticated by this certificate. See also usage of property ``org.obiba.opal.security.ssl.allowInvalidCertificates`` in :ref:`misc-config`.

Data Schemas
------------

Depending on the database engine and usage, an administrator will be asked to specify how the data will be organized in the database. See :doc:`../../variables-data` documentation for a description of the Opal's data model. This data model can be persisted in different data schemas depending on the usage.

.. _opal-sql:

Opal SQL
~~~~~~~~

The purpose of this SQL data schema is to be able to accommodate any number of variables from the Opal table abstraction point of view. A SQL-table will have a limit in terms of number of columns that can be added (this limit depends on the database engine). The Opal SQL schema follows the `Entity-attribute-value <https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model>`_ model (EAV), which allows to describe Opal tables with thousands of variables. However the price of the EAV schema is that querying data requires a lot of SQL join requests. Opal tries its best by caching SQL query results but there is still a performance price for this flexibility.

You may choose this data schema when:

* the number of expected variables is large (more than several hundreds),
* flexibility is preferred to performance.

.. _tabular-sql:

Tabular SQL
~~~~~~~~~~~

The Tabular SQL schema propose a more standard representation of the data: there is one SQL table per Opal table (and therefore one column per variable). Querying such schema is very straightforward but data persistence has some limits:

* the number of columns in a SQL table and/or the size of each row are limited (and therefore the number of variables in a Opal table). This number depends on the database engine. In the case of MySQL there is a hard limit of 4096 columns per table but the effective limit depends on the size of the rows that are being persisted. For more information see `Limits on Table Column Count and Row Size <http://dev.mysql.com/doc/refman/5.6/en/column-count-limit.html>`_ in MySQL documentation or the `About PostgreSQL <http://www.postgresql.org/about/>`_ documentation.
* the name conflicts between variables (resp. tables) are more likely to occur as characters used for naming objects and length of the names are limited: see `Schema Object Names <https://dev.mysql.com/doc/refman/5.0/en/identifiers.html>`_ and `Identifier Case Sensitivity <https://dev.mysql.com/doc/refman/5.0/en/identifiers.html>`_ in MySQL documentation or `Identifiers and Key Words <https://dev.mysql.com/doc/refman/5.0/en/identifiers.html>`_ in PostgreSQL documentation.
* the generated SQL type may not be optimal for some data. For instance the text type does not have data length constraint: this affects the row size although some data could be short text. Also binary values are stored in a column with `BLOB <https://dev.mysql.com/doc/refman/5.0/en/blob.html>`_ (or `bytea <http://www.postgresql.org/docs/9.0/static/datatype-binary.html>`_) type which data size can be limited.

On the other hand this data schema still worth to be chosen when:

* the number of variables is limited (less than several hundreds, modulo the data size of each row),
* queries involving vector need to be fast (data summary of a variable, assignment to a R dataframe),
* import of an existing SQL table,
* export to a SQL table.

Opal offers to specify some settings for this schema:


.. list-table::
   :header-rows: 1

   * - Setting
     - Description
     - Remark
   * - Entity Identifier Column
     - | Name of the column containing the identifier of the entity in the SQL-table. This column will not be considered as a variable.
       | This identifier column is a primary key, i.e. there must be only one row with a given identifier (same rule applies to a CSV file).
       | Only the SQL-tables having this column can be mapped to a Opal table.
     - | Required, value is *opal_id* when usage is
       | *storage*.
   * - Creation Timestamp Column
     - | Name of the column holding the timestamp of the creation of a row in the SQL-table. This is a purely informative information that
       | makes sense only when data are subsequently updated.
     - | Optional, value is *opal_created* when usage is
       | *storage*.
   * - Update Timestamp Column
     - | Name of the column holding the timestamp of the last modification date of a row in the SQL-table. This information can be useful
       | when performing an incremental import (only new or updated rows are imported).
     - | Optional, recommended for *import*/*export*, value
       | is *opal_updated* when usage is *storage*.
   * - With variables description tables
     - | In addition to the SQL tables of data, the data dictionary can be persisted in other SQL tables: value_tables, variables,
       | variable_attributes, categories and category_attributes. This allow to have fully described data (otherwise the data dictionary is
       | limited to the column names and SQL types).
     - | Optional, recommended for *import*/*export*,
       | selected when usage is *storage*.
   * - Default Entity Type
     - When there is no variables description tables, this setting specifies the entity type of the tables that are discovered.
     - Required.

The mapping beween the `SQL types <http://docs.oracle.com/javase/8/docs/api/java/sql/Types.html>`_ and the Opal value types is the following:

====================================== =================
SQL Type                               Value Type
====================================== =================
BIGINT, INTEGER, SMALLINT, TINYIN      integer
DECIMAL, DOUBLE, FLOAT, NUMERIC, REAL  decimal
DATE                                   date
TIMESTAMP                              datetime
BIT, BOOLEAN                           boolean
BLOB, LONGVARBINARY, VARBINARY, BINARY binary
anything else                          text
====================================== =================

Limesurvey
~~~~~~~~~~

Opal is able to read directly the SQL data schema of a `Limesurvey <https://www.limesurvey.org/>`_ server. Opal will detect the completed interviews and will import the new and updated ones. The variables are also extracted from the Limesurvey questionnaire.

Operations
----------

Register
~~~~~~~~

Registering a database requires to specify:

* the database engine,
* a unique name for identification when creating a project or importing/exporting,
* the connection details: jdbc url and credentials (user name, password),
* the usage (applies to SQL database engine only),
* the data schema (applies to SQL database engine only, choice is limited by selected usage),
* optional properties (key, value pairs).

Depending on the database engine, the declared usage and the data schema some options may be available or not.

Several databases can be registered for storage usage. All databases support the persistence of multiple projects. At project creation, the database where the project's data will be persisted is to be chosen.

Unregister
~~~~~~~~~~

A database used for storage cannot be unregistered if there are still projects linked to it. If this is the case, remove or archive the corresponding projects and then unregister the database (any remaining data will be untouched).

Edit
~~~~

Limited edition of the database is possible when a database is in production.

Test
~~~~

Opal server reports the result of a connection attempt. This allows to validate the connection url and credentials. This does not verifies that the database permissions are appropriate for the declared usage.
