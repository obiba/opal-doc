Export SAS (R)
==============

Export in SAS or SAS Transport format in Opal file system.

.. note::

  Prefer the SAS Transport format (``.xpt``). The ``.sas7bdat`` export relies on the ``write_sas()`` function of the `haven <https://haven.tidyverse.org/>`_ R package, which is deprecated in favour of ``write_xpt()``.

Variable names that are not valid in these formats are adjusted in the exported file: characters other than ASCII letters, digits and underscores are replaced by an underscore, a leading digit is prefixed by an underscore and names are limited to 32 characters.

.. code-block:: bash

  opal export-r-sas <CREDENTIALS> <OPTIONS> [EXTRAS]

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
     - Output SAS or SAS Transport file name on the Opal file system

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Export table from opal-data to a SAS Transport file:

.. code-block:: bash

  opal export-r-sas --opal https://opal-demo.obiba.org --user administrator --password password --datasource opal-data --tables StandingHeight --output /tmp/sh.xpt
