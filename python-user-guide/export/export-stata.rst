Export Stata (R)
================

Export in Stata format in Opal file system.

.. code-block:: bash

  opal export-r-stata <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--id-name ID_NAME, -in ID_NAME``
     - ID column name (optional)
   * - ``--output OUTPUT, -out OUTPUT``
     - Output Stata file name on the Opal file system

.. include:: ../common-credentials.rst

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

Export table from opal-data to a Stata file:

.. code-block:: bash

  opal export-r-stata --opal https://opal-demo.obiba.org --user administrator --password password --datasource opal-data --tables StandingHeight --output /tmp/sh.dta
