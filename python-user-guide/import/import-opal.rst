Import Opal
===========

Import from a remote opal server.

.. code-block:: bash

  opal import-opal <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--destination DESTINATION, -d DESTINATION``
     - Destination datasource name
   * - ``--tables TABLES [TABLES ...], -t TABLES [TABLES ...]``
     - The list of tables to be imported (defaults to all)
   * - ``--incremental -i``
     - Incremental import
   * - ``--identifiers IDENTIFIERS, -id IDENTIFIERS``
     - Name of the ID mapping
   * - ``--policy POLICY, -po POLICY``
     - | ID mapping policy:
       |
       | ``required`` : each identifiers must be mapped prior importation (default),
       | ``ignore`` : ignore unknown identifiers,
       | ``generate`` : generate a system identifier for each unknown identifier.
   * - ``--ropal ROPAL, -ro ROPAL``
     - Remote Opal server base url
   * - ``--ruser RUSER, -ru RUSER``
     - Remote User name to connect to Opal
   * - ``--rpassword RPASSWORD, -rp RPASSWORD``
     - Remote User's password
   * - ``--key KEY, -k KEY``
     - Location of the certificate key
   * - ``--rdatasource RDATASOURCE, -rd RDATASOURCE``
     - Remote datasource name

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

Copy tables BloodPressure and ArmSpan from Opal on demo.obiba.org to Opal on localhost:

.. code-block:: bash

  opal import-opal -o http://localhost:8080 -u administrator -p password  --ro https://opal-demo.obiba.org --ru administrator --rp password --rdatasource onyx --destination opal-data --tables BloodPressure ArmSpan
