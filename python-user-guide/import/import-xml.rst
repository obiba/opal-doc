Import Opal Archive
===================

Import an archive of XML files, to be found in Opal file system.

.. code-block:: bash

  opal import-spss <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--path PATH -pa PATH``
     - Path to the zip of XML files to import on the Opal file system
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import tables from 20-onyx ZIP file to the opal-data datasource:

.. code-block:: bash

  # Import all tables
  opal import-xml --opal https://opal-demo.obiba.org --user administrator --password password --path /home/administrator/20-onyx-data.zip --destination opal-data

  # Import only ArmSpan and BloodPressure tables
  opal import-xml --opal https://opal-demo.obiba.org --user administrator --password password --path /home/administrator/20-onyx-data.zip --destination opal-data --tables ArmSpan --tables BloodPressure
