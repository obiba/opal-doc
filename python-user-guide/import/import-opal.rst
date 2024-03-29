Import Opal
===========

Import from a remote opal server.

.. code-block:: bash

  opal import-opal <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--ropal ROPAL, -ro ROPAL``
     - Remote Opal server base url
   * - ``--ruser RUSER, -ru RUSER``
     - Remote user name (exclusive from using token)
   * - ``--rpassword RPASSWORD, -rp RPASSWORD``
     - Remote user password (exclusive from using token)
   * - ``--rtoken RTOKEN, -rt RTOKEN``
     -  Remote personal access token (exclusive from user credentials)
   * - ``--rdatasource RDATASOURCE, -rd RDATASOURCE``
     - Remote datasource name
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Copy tables BloodPressure and ArmSpan from Opal on demo.obiba.org to Opal on localhost:

.. code-block:: bash

  opal import-opal -o http://localhost:8080 -u administrator -p password  --ro https://opal-demo.obiba.org --ru administrator --rp password --rdatasource onyx --destination opal-data --tables BloodPressure ArmSpan
