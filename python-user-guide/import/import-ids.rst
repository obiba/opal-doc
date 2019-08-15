Import System Identifiers
=========================

Import entity system identifiers.

.. code-block:: bash

  opal import-ids <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--type TYPE, -t TYPE``
     - Entity type of the data (e.g. Participant)

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

Import system identifiers from keyboard entries.

.. code-block:: bash

  opal import-ids --opal https://opal-demo.obiba.org --user administrator --password password --type Participant

Import system identifiers from a file.

.. code-block:: bash

  opal import-ids --opal https://opal-demo.obiba.org --user administrator --password password --type Participant < ids.txt

Example of a file of identifiers:

.. code-block:: text

  11123456
  11345467
  11995884
  11423423
