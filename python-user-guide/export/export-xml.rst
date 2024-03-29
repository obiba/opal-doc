Export Opal Archive
===================

Export in XML format in Opal file system.

.. code-block:: bash

  opal export-xml <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--datasource DATASOURCE, -d DATASOURCE``
     - Datasource name
   * - ``--tables TABLES [TABLES ...], -t TABLES [TABLES ...]``
     - The list of tables to be exported
   * - ``--incremental -i``
     - Incremental export
   * - ``--identifiers ID_MAPPING, -id ID_MAPPING``
     - Entity ID mapping name
   * - ``--output OUTPUT, -out OUTPUT``
     - Output zip file name on the Opal file system

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Export tables from opal-data to a ZIP file of XML files:

.. code-block:: bash

  opal export-xml --opal https://opal-demo.obiba.org --user administrator --password password --datasource opal-data --tables Spirometry StandingHeight --output /tmp/export.zip
