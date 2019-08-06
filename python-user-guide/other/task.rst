Task
====

Manage a task, for shell scripts submitting tasks (import/export) and waiting for their completion.

.. code-block:: bash

  opal task <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

========================= ====================================
Option                    Description
========================= ====================================
``--id ID``               The task ID. If not provided, it will be read from the standard input (from the JSON representation of the task or a plain value).
``--show, -sh``           Show JSON representation of the task
``--status, -st``         Get the status of the task
``--wait, -w``            Wait for the task to complete (successfully or not)
``--cancel, -c``          Cancel the task
``--delete, -d``          Delete the task
========================= ====================================

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
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

Get the full status of a task:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --json

Get the status token of a task:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --status

Wait for the task to complete and get its status token:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --wait
