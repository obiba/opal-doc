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

Authentication can be done by username/password credentials OR by personal access token OR by certificate/private key pair (two-way SSL authentication).

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url
``--user USER, -u USER``              Credentials auth: user name (requires a password)
``--password PASSWORD, -p PASSWORD``  Credentials auth: user password (requires a user name)
``--token TOKEN, -tk TOKEN``          Token auth: User access token
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Two-way SSL auth: certificate/public key file (requires a private key)
``--ssl-key SSL_KEY, -sk SSL_KEY``    Two-way SSL auth: private key file (requires a certificate)
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
