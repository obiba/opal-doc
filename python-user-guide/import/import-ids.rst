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
