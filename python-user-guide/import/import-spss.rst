Import SPSS
===========

Import a SPSS file, to be found in Opal file system.

.. code-block:: bash

  opal import-xml <CREDENTIALS> <OPTIONS> [EXTRAS]

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
     - Path to the SPSS file to import on the Opal file system
   * - ``--locale LOCALE, -l LOCALE``
     - Language code to be associated to labels
   * - ``--characterSet CHARACTERSET, -c CHARACTERSET``
     - Character set to be used when reading the file
   * - ``--type TYPE, -ty TYPE``
     - Entity type (default is Participant)
   * - ``--idVariable IDVARIABLE, -iv IDVARIABLE``
     - SPSS variable that provides the entity ID. If not specified, first variable values are considered to be the entity identifiers.
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

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

Import table from RobotChicken SPSS file in opal-data datasource:

.. code-block:: bash

  opal import-spss --opal https://opal-demo.obiba.org --user administrator --password password --destination opal-data --characterSet ISO-8859-1 --locale en --path /home/administrator/RobotChicken.sav
