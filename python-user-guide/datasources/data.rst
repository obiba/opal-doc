Data
====

Get data: list of entity identifiers or entity values from a table/variable.

.. code-block:: bash

  opal data <RESOURCE> <CREDENTIALS> [EXTRAS]

Arguments
---------

============= ===========
Argument      Description
============= ===========
``RESOURCE``	Resource identification in the format ``<datasource>.<table>[:<variable>]``. Each project has a datasource which is identified by the project's name.
============= ===========

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

Fetch the list of entity identifiers associated to a table:

.. code-block:: bash

  opal data datashield.CNSIM1 --opal https://opal-demo.obiba.org --user administrator --password password

Fetch the variable value for a entity in a table:

.. code-block:: bash

  # Get the JSON representation of all participant values in a table
  opal data datashield.CNSIM1 -o https://opal-demo.obiba.org -u administrator -p password --id 9553295965 -j

  # Get the JSON representation of a variable value
  opal data datashield.CNSIM1:GENDER -o https://opal-demo.obiba.org -u administrator -p password --id 9553295965 -j

  # Get the raw value. If variable is of binary type, a byte stream is outputed.
  opal data datashield.CNSIM1:GENDER -o https://opal-demo.obiba.org -u administrator -p password --id 9553295965 -j --raw
