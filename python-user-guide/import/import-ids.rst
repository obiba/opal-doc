Import System Identifiers
=========================

Import entity system identifiers.

.. code-block:: bash

  opal import-ids <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--type TYPE, -t TYPE``
     - Entity type of the data (e.g. Participant)

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import system identifiers from keyboard entries.

.. code-block:: bash

  opal import-ids --opal https://opal-demo.obiba.org --user administrator --password password --type Participant

Import system identifiers from a file.

.. code-block:: bash

  opal import-ids --opal https://opal-demo.obiba.org --user administrator --password password --type Participant < ids.txt

Example of a file of identifiers:

.. code-block:: text

  11123456
  11345467
  11995884
  11423423
