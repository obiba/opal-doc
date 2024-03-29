Import SAS (R)
==============

Import a SAS or SAS Transport file, to be found in Opal file system, using R.

.. code-block:: bash

  opal import-r-sas <CREDENTIALS> <OPTIONS> [EXTRAS]

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
     - Path to the SAS or SAS Transport file to import on the Opal file system
   * - ``--locale LOCALE, -l LOCALE``
     - Language code to be associated to labels
   * - ``--type TYPE, -ty TYPE``
     - Entity type (default is Participant)
   * - ``--idVariable IDVARIABLE, -iv IDVARIABLE``
     - SAS variable that provides the entity ID. If not specified, first variable values are considered to be the entity identifiers.
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import table from RobotChicken SAS file in opal-data datasource:

.. code-block:: bash

  opal import-r-sas --opal https://opal-demo.obiba.org --user administrator --password password --destination opal-data --locale en --path /home/administrator/RobotChicken.sas7bdat
