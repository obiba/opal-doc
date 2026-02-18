Export RDS (R)
==============

Export in RDS format in Opal file system. A RDS file contains a single serialized R object, which will be a `tibble <https://tibble.tidyverse.org/>`_ and that can be read in R using `base::readRDS() <https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/readRDS>`_.


.. code-block:: bash

  opal export-r-rds <CREDENTIALS> <OPTIONS> [EXTRAS]

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
   * - ``--output OUTPUT, -out OUTPUT``
     - Output RDS file name on the Opal file system

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Export table from opal-data to a RDS file:

.. code-block:: bash

  opal export-r-rds --opal https://opal-demo.obiba.org --user administrator --password password --datasource CNSIM --tables CNSIM1 --output /tmp/cnsim1.rds
