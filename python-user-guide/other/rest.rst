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

Get the list of all datasources:

.. code-block:: bash

  opal rest /datasources --opal https://opal-demo.obiba.org --user administrator --password password --json

Get the list of all tables of datasource 'medications':

.. code-block:: bash

  opal rest /datasource/medications/tables --opal https://opal-demo.obiba.org --user administrator --password password --json

Get the list of tables with entity id '6397957' of type 'Participant':

.. code-block:: bash

  opal rest /entity/6397957/type/Participant/tables --opal https://opal-demo.obiba.org --user administrator --password password --json
