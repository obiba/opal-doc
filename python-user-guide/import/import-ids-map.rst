Import Identifiers Mapping
==========================

Import Opal server entity identifiers.

.. code-block:: bash

  opal import-ids-map <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--type TYPE, -t TYPE``
     - Entity type of the data (e.g. Participant)
   * - ``--map MAP, -m MAP``
     - Mapping name, i.e. the name associated to the identifiers that will be mapped to the system identifiers
   * - ``--separator SEP, -s SEP``
     - Identifiers separator (default is ",")

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import identifiers mapping from keyboard entries.

.. code-block:: bash

  opal import-ids-map --opal https://opal-demo.obiba.org --user administrator --password password --type Participant --map foo

Import identifiers mapping from a file.

.. code-block:: bash

  opal import-ids-map --opal https://opal-demo.obiba.org --user administrator --password password --type Participant --map foo < idsmap.txt

Example of a file of identifiers mapping:

.. code-block:: text

  11123456,A11111
  11345467,A22222
  11995884,A33333
  11423423,A44444
