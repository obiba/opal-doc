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

Get the list of groups with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch

Get a specific group with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch --name editor

Delete the group study_editor

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --delete --name study_editor
