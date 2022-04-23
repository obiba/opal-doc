Import LimeSurvey
=================

Import from a remote LimeSurvey server.

.. code-block:: bash

  opal import-limesurvey <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--database DATABASE, -db DATABASE``
     - Name of the LimeSurvey SQL database as registered in Opal
   * - ``--prefix PREFIX -pr PREFIX``
     - Table prefix of LimeSurvey tables (default: none)
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import the table "Withdrawal Script (WaveInter-wave contact)" from LimeSurvey database to the opal-data datasource:

.. code-block:: bash

  opal import-limesurvey --opal https://opal-demo.obiba.org --user administrator --password password --destination ds1 --database LimeSurvey --json -t "Withdrawal Script (WaveInter-wave contact)"
