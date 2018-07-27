System
======

Query for system status and configuration.

.. code-block:: bash

  opal system <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

================ ====================================
Option           Description
================ ====================================
``--conf``       Opal application configuration (default option)
``--version``    Opal version number
``--status``     Opal application status (JVM related dynamic properties)
================ ====================================

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

Retrieve Opal configuration information:

.. code-block:: bash

  opal system --opal https://opal-demo.obiba.org --user administrator --password password --conf

Retrieve Opal version number:

.. code-block:: bash

  opal system --opal https://opal-demo.obiba.org --user administrator --password password --version

Retrieve Opal status and JVM related dynamic properties:

.. code-block:: bash

  opal system --opal https://opal-demo.obiba.org --user administrator --password password --status

Retrieve Opal java execution environment its JVM relates statistics properties:

.. code-block:: bash

  opal system --opal https://opal-demo.obiba.org --user administrator --password password --env
