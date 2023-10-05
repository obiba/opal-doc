Data Dictionary
===============

Get metadata: datasources, tables or variables.

.. code-block:: bash

  opal dict <RESOURCE> <CREDENTIALS> [EXTRAS]

Arguments
---------

============= ===========
Argument      Description
============= ===========
``RESOURCE``	Resource identification in the format ``<datasource>[.<table>[:<variable>]]``. Wild card * is supported. Each project has a datasource which is identified by the project's name.
============= ===========


Options
---------

================= ===========
Option            Description
================= ===========
``--excel, -xls``	Excel file path that will contain variables metadata. The ``RESOURCE`` must be of ``<datasource>.<table>:*`` format.
================= ===========

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

To fetch the dictionary associated to a datasource:

.. code-block:: bash

  opal dict datashield --opal https://opal-demo.obiba.org --user administrator --password password

To fetch the dictionary associated to a table in a pretty format:

.. code-block:: bash

  opal dict CNSIM.CNSIM1 --opal https://opal-demo.obiba.org --user administrator --password password -j

To fetch the description of a variable:

.. code-block:: bash

  opal dict CNSIM.CNSIM1:PM_BMI_CONTINUOUS -o https://opal-demo.obiba.org -u administrator -p password -j

Wild cards can also be used:

.. code-block:: bash

  # Get all datasources
  opal dict "*" --opal https://opal-demo.obiba.org --user administrator --password password

  # Get all tables from datashield datasource
  opal dict "datashield.*" --opal https://opal-demo.obiba.org --user administrator --password password

  # Get all variables CNSIM.CNSIM1 table
  opal dict "CNSIM.CNSIM1:*" --opal https://opal-demo.obiba.org --user administrator --password password

  # Get all variables CNSIM.CNSIM1 table in Excel format
  opal dict "CNSIM.CNSIM1:*" --opal https://opal-demo.obiba.org --user administrator --password password --excel /tmp/CNSIM1.xlsx
