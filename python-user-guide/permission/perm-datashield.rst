DataSHIELD Permission
=====================

Manage DataSHIELD usage permissions.

.. code-block:: bash

  opal perm-datashield <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``, ``use``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
==================================== =====================================

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

Add use permission for subject demouser:

.. code-block:: bash

  opal perm-datashield --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission use --add

Remove the above permission:

.. code-block:: bash

  opal perm-datashield --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --delete
