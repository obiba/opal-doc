Web Services
============

This command is for advanced users wanting to directly access to the REST API of Opal server.

.. code-block:: bash

  opal rest <PATH> <CREDENTIALS> [OPTIONS] [EXTRAS]

Arguments
---------

======== ===========
Argument Description
======== ===========
``PATH`` Web service path, for instance: /project/xxx
======== ===========

Options
-------

================================================= ====================================
Option                                            Description
================================================= ====================================
``--method METHOD, -m METHOD``                    HTTP method: GET (default), POST, PUT, DELETE, OPTIONS.
``--accept ACCEPT, -a ACCEPT``                    Accept header (default is application/json).
``--content-type CONTENT_TYPE, -ct CONTENT_TYPE`` Content-Type header (default is application/json).
``--headers HEADERS, -hs HEADERS``                Custom headers in the form of: { "Key2": "Value2", "Key2": "Value2" }
================================================= ====================================

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

Get the list of all datasources:

.. code-block:: bash

  opal rest /datasources --opal https://opal-demo.obiba.org --user administrator --password password --json

Get the list of all tables of datasource 'medications':

.. code-block:: bash

  opal rest /datasource/medications/tables --opal https://opal-demo.obiba.org --user administrator --password password --json

Get the list of tables with entity id '6397957' of type 'Participant':

.. code-block:: bash

  opal rest /entity/6397957/type/Participant/tables --opal https://opal-demo.obiba.org --user administrator --password password --json
