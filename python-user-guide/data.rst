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
