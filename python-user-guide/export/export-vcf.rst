Export VCF
==========

Export VCF files in Opal file system.

.. code-block:: bash

  opal export-vcf <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--project PROJECT, -pr PROJECT``
     - Project name from which genotypes data will be exported
   * - ``--vcf FILE01 FILE02, -vcf FILE01 FILE02``
     - List of VCF/BCF file names
   * - ``--destination DESTINATION, -d DESTINATION``
     - Destination folder (in Opal file system)
   * - ``--filter-table FILTER -f FILTER``
     - Participant table name to be used to filter the samples by participant ID (only relevant if there is a sample-participant mapping defined)
   * - ``--no-case-controls, -nocc``
     - Do not include case control samples (only relevant if there is a sample-participant mapping defined)

.. include:: ../common-credentials.rst

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

Export VCF files into the user's export directory, omitting control samples:

.. code-block:: bash

  opal export-vcf --opal https://opal-demo.obiba.org --user administrator --password password --project TEST --vcf FILE01 FILE02 --destination /home/administrator/export --filter-table TEST.mapping --no-case-controls
