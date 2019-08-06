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

To fetch the dictionary associated to a datasource:

.. code-block:: bash

  opal dict datashield --opal https://opal-demo.obiba.org --user administrator --password password

To fetch the dictionary associated to a table in a pretty format:

.. code-block:: bash

  opal dict datashield.CNSIM1 --opal https://opal-demo.obiba.org --user administrator --password password -j

To fetch the description of a variable:

.. code-block:: bash

  opal dict datashield.CNSIM1:PM_BMI_CONTINUOUS -o https://opal-demo.obiba.org -u administrator -p password -j

Wild cards can also be used:

.. code-block:: bash

  # Get all datasources
  opal dict "*" --opal https://opal-demo.obiba.org --user administrator --password password

  # Get all tables from datashield datasource
  opal dict "datashield.*" --opal https://opal-demo.obiba.org --user administrator --password password

  # Get all variables datashield.CNSIM1 table
  opal dict "datashield.CNSIM1:*" --opal https://opal-demo.obiba.org --user administrator --password password
