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
   * - ``--vcf FILE01 FILE02, -vcf FILE01 FILE02``
     - List of VCF/BCF (optionally compressed) file paths (in Opal file system)

Credentials
-----------

Authentication is done by username/password credentials.

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url.
``--user USER, -u USER``              User name. User with appropriate permissions is expected depending of the REST resource requested.
``--password PASSWORD, -p PASSWORD``  User password.
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Path to the certificate (public key) file
``--ssl-key SSL_KEY, -sk SSL_KEY``    Path to the private key file
===================================== ====================================

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

Import VCF files into the project TEST:

.. code-block:: bash

  opal import-vcf --opal https://opal-demo.obiba.org --user administrator --password password --project TEST --vcf /path/to/file01.vcf.gz /path/to/file02.vcf.gz
