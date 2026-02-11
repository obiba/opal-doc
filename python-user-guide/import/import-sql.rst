Import SQL
==========

Import from a remote SQL server.

.. code-block:: bash

  opal import-sql <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--destination DESTINATION, -d DESTINATION``
     - Destination datasource name
   * - ``--tables TABLE1 [--tables TABLE2 ...], -t TABLE1 [-t TABLE2 ...]``
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
   * - ``--database DATABASE, -db DATABASE``
     - Name of the SQL database as registered in Opal
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import the table "AnkleBrachial" from a SQL database to the opal-data datasource:

.. code-block:: bash

  opal import-sql --opal https://opal-demo.obiba.org --user administrator --password password --destination ds1 --database sql_db --json -t AnkleBrachial
