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

Authentication can be done by username/password credentials OR by personal access token OR by certificate/private key pair (two-way SSL authentication).

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url
``--user USER, -u USER``              Credentials auth: user name (requires a password)
``--password PASSWORD, -p PASSWORD``  Credentials auth: user password (requires a user name)
``--token TOKEN, -tk TOKEN``          Token auth: User access token
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Two-way SSL auth: certificate/public key file (requires a private key)
``--ssl-key SSL_KEY, -sk SSL_KEY``    Two-way SSL auth: private key file (requires a certificate)
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
