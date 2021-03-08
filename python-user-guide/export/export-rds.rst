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
   * - ``--tables TABLES [TABLES ...], -t TABLES [TABLES ...]``
     - The list of tables to be exported
   * - ``--incremental -i``
     - Incremental export
   * - ``--identifiers ID_MAPPING, -id ID_MAPPING``
     - Entity ID mapping name
   * - ``--id-name ID_NAME, -in ID_NAME``
     - ID column name (optional)
   * - ``--output OUTPUT, -out OUTPUT``
     - Output RDS file name on the Opal file system

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

Export table from opal-data to a RDS file:

.. code-block:: bash

  opal export-r-rds --opal https://opal-demo.obiba.org --user administrator --password password --datasource CNSIM --tables CNSIM1 --output /tmp/cnsim1.rds
