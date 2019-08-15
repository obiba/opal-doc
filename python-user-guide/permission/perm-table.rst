Table Permission
================

Manage permissions on a project's table.

.. code-block:: bash

  opal perm-table <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

===================================================== =====================================
Option                                                Description
===================================================== =====================================
``--add, -a``                                         Add a permission
``--delete, -d``                                      Delete a permission
``--permission PERM, -pe PERM``                       Permission to apply: ``view``, ``view-value``, ``edit``, ``edit-values``, ``administrate``
``--subject SUBJECT, -s SUBJECT``                     Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``                             Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                    Project name on which the permission is to be set
``--tables TABLE [TABLE ...], -t TABLE [TABLE ...]``  List of table names on which the permission is to be set (default is all)
===================================================== =====================================

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
``--json, -j``    Output pretty-print JSON
================= =================

Example
-------

Add view permission for subject demouser on table CNSIM1 in datashield project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project datashield --subject demouser  --permission view --add --tables CNSIM1

Remove the above permission:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project datashield --subject demouser --delete --table CNSIM1

Add permission on all tables of datashield project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project datashield --subject demouser --permission view --add

Remove permission from all table of datashield project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project datashield --subject demouser --delete

Add permission on specific tables:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project datashield --subject demouser --permission view --add --tables CNSIM1 FNAC
