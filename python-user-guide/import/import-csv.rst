Import CSV
==========

Import a CSV file, to be found in Opal file system.

.. code-block:: bash

  opal import-csv <CREDENTIALS> <OPTIONS> [EXTRAS]

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
     - Path to the CSV file to import on the Opal file system
   * - ``--characterSet CHARACTERSET, -c CHARACTERSET``
     - Character set of the file (e.g utf-8)
   * - ``--separator SEPARATOR, -s SEPARATOR``
     - Field separator
   * - ``--quote QUOTE, -q QUOTE``
     - Quotation mark character
   * - ``--firstRow FIRSTROW, -f FIRSTROW``
     - Number of the first row that contains data to import
   * - ``--type TYPE, -ty TYPE``
     - Entity type of the data (e.g. Participant)
   * - ``--valueType VALUETYPE, -vt VALUETYPE``
     - Default value type (text, integer, decimal, boolean etc.). When not specified, "text" is the default.


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

Import catchment areas from a csv file delimited with ',' :

.. code-block:: bash

  opal import-csv --opal https://opal-demo.obiba.org --user administrator --password password --destination opal-data --path /home/administrator/catchment-area.csv --tables catchment-area --separator , --type Area
