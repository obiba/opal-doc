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
