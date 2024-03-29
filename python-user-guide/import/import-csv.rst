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
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).


.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import catchment areas from a csv file delimited with ',' :

.. code-block:: bash

  opal import-csv --opal https://opal-demo.obiba.org --user administrator --password password --destination opal-data --path /home/administrator/catchment-area.csv --tables catchment-area --separator , --type Area
