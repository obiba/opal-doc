System Permission
=================

Manage global system permissions.

.. code-block:: bash

  opal perm-system <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``, ``add-project``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
==================================== =====================================

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
``--json, -j``    Output pretty-print JSON
================= =================

Example
-------

Add add-project permission for subject demouser:

.. code-block:: bash

  opal perm-system --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission add-project --add

Remove the above permission:

.. code-block:: bash

  opal perm-system --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --delete
