Group
=====

Manage a group in the Opal internal user directory.

.. code-block:: bash

  opal group <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

========================== =====================================
Option                     Description
========================== =====================================
``--name NAME, -n NAME``   Group name
``--fetch, -f``            Fetch a user (all groups are returned if no option --name is given)
``--delete, -de``          Delete the group specified by the --name option
========================== =====================================

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

Get the list of groups with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch

Get a specific group with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch --name editor

Delete the group study_editor

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --delete --name study_editor
