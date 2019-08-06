Restore Views
=============

Restore views that were previously backed up in the local file system into a project. The expected format of the
view files is JSON. If one or more tables that are referenced by the backed up view do not exist anymore, the restoration will fail.

.. code-block:: bash

  opal restore-view <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
==================================================== =====================================
Option                                               Description
==================================================== =====================================
``--project PROJECT, -pr PROJECT``	                 Destination project name
``--views VIEWS [VIEWS ...], -vw VIEWS [VIEWS ...]`` List of view names to be restored (default is all the JSON files that are found in the backup directory)
``--input INPUT, -in INPUT``                         Input directory name (default is current directory)
``--force, -f``                                      Skip confirmation when overwriting an existing view.
==================================================== =====================================

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

Restore a specific view file ``CNSIM.json`` into a project:

.. code-block:: bash

  opal restore-view --opal https://opal-demo.obiba.org --user administrator --password password --project datashield --views CNSIM
