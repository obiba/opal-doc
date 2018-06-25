Table Copy
==========

Launch a task that will perform a table copy from one project to another. The destination project can be the one of origin in which case the table has to be renamed.

.. code-block:: bash

  opal copy-table <CREDENTIALS> [OPTIONS] [XTRAS]
  
Options
-------
===================== =====================================
Option                Description
===================== =====================================
``--project, -pr``	  Source project name
``--tables, -t``	    List of table names which will be copied (default is all)
``--destination, -d``	Destination project name
``--name, -na``	      New table name (required if source and destination are the same, ignored if more than one table is to be copied)
``--incremental, -i`` Incremental copy
``--nulls, -nu``	    Copy the null values
===================== =====================================

Credentials
-----------

Authentication is done by username/password credentials.

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url.
``--user USER, -u USER``              User name. User with appropriate permissions is expected depending of the REST resource requested.
``--password PASSWORD, -p PASSWORD``  User password.
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Path to the certificate (public key) file
``--ssl-key SSL_KEY, -sk SSL_KEY``    Path to the private key file
===================================== ====================================

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

Copy a table in the same project, by specifying a new name:

.. code-block:: bash

  opal copy-table --opal https://opal-demo.obiba.org --user administrator --password password --project datashield --tables CNSIM1 --destination datashield --name CNSIM4
