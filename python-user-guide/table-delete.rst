Table Delete
============

Delete one or more tables of a project.

.. code-block:: bash

  opal delete-table <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
===================== =====================================
Option                Description
===================== =====================================
``--project, -pr``	  Source project name
``--tables, -t``	    List of table names which will be deleted (default is all)
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
================= =================

Example
-------

Delete some tables from a project:

.. code-block:: bash

  opal delete-table --opal https://opal-demo.obiba.org --user administrator --password password --project project_test --tables Table1 Table2

Delete all tables from a project:

.. code-block:: bash

  opal delete-table --opal https://opal-demo.obiba.org --user administrator --password password --project project_test
