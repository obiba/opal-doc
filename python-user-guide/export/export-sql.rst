Export SQL
==========

Export in a SQL database.

.. code-block:: bash

  opal export-sql <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--datasource DATASOURCE, -d DATASOURCE``
     - Datasource name
   * - ``--tables TABLE1 [--tables TABLE2 ...], -t TABLE1 [-t TABLE2 ...]``
     - The list of tables to be exported
   * - ``--incremental -i``
     - Incremental export
   * - ``--identifiers ID_MAPPING, -id ID_MAPPING``
     - Entity ID mapping name
   * - ``--database DATABASE, -db DATABASE``
     - Name of the SQL database as registered in Opal

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Export tables from opal-data to a SQL database:

.. code-block:: bash

  opal export-sql --opal https://opal-demo.obiba.org --user administrator --password password --datasource opal-data --tables Spirometry  --database sql_db
