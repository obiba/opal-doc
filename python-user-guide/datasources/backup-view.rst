Backup Views
============

Backup named or all views of a project in the local file system. If the backup directory does not exist, it will be created.
The views are stored as JSON files. Permissions that may have been setup are not backed up.

.. code-block:: bash

  opal backup-view <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
==================================================== =====================================
Option                                               Description
==================================================== =====================================
``--project PROJECT, -pr PROJECT``                   Source project name
``--views VIEWS [VIEWS ...], -vw VIEWS [VIEWS ...]`` List of view names to be backed up (default is all)
``--output OUTPUT, -out OUTPUT``                     Output directory name (default is current directory)
``--force, -f``                                      Skip confirmation when overwriting the backup file.
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

Backup a specific view from a project into file ``CNSIM.json``:

.. code-block:: bash

  opal backup-view --opal https://opal-demo.obiba.org --user administrator --password password --project datashield --views CNSIM
