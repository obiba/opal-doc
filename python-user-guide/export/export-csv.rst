Export CSV
==========

Export in CSV format in Opal file system.

.. code-block:: bash

  opal export-csv <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--id-name ID_NAME, -in ID_NAME``
     - ID column name (optional)
   * - ``--no-multilines, -nl``
     - Do not write value sequences as multiple lines
   * - ``--output OUTPUT, -out OUTPUT``
     - Output directory name on the Opal file system

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Export tables from opal-data. A subdirectory is created with table definition and data as CSV files.

.. code-block:: bash

  opal export-csv --opal https://opal-demo.obiba.org --user administrator --password password --datasource opal-data --tables BloodPressure --output /tmp/export
