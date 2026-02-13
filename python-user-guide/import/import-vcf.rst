Import VCF
==========

Import VCF file(s) from Opal file system. Requires that the destination project has a VCF store activated.

.. code-block:: bash

  opal import-vcf <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--project PROJECT, -pr PROJECT``
     - Project name into which genotypes data will be imported
   * - ``--vcf FILE01 --vcf FILE02``
     - List of VCF/BCF (optionally compressed) file paths (in Opal file system)

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import VCF files into the project TEST:

.. code-block:: bash

  opal import-vcf --opal https://opal-demo.obiba.org --user administrator --password password --project TEST --vcf /path/to/file01.vcf.gz --vcf /path/to/file02.vcf.gz
