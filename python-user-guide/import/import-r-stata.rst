Import Stata (R)
================

Import a Stata file, to be found in Opal file system, using R.

.. code-block:: bash

  opal import-r-stata <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--path PATH -pa PATH``
     - Path to the Stata file to import on the Opal file system
   * - ``--locale LOCALE, -l LOCALE``
     - Language code to be associated to labels
   * - ``--type TYPE, -ty TYPE``
     - Entity type (default is Participant)
   * - ``--idVariable IDVARIABLE, -iv IDVARIABLE``
     - Stata variable that provides the entity ID. If not specified, first variable values are considered to be the entity identifiers.

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
Import table from RobotChicken Stata file in opal-data datasource:

.. code-block:: bash

  opal import-r-stata --opal https://opal-demo.obiba.org --user administrator --password password --destination opal-data --locale en --path /home/administrator/RobotChicken.dta