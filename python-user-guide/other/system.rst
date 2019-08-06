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
