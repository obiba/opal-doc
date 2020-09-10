Entity
======

Get entity information.

.. code-block:: bash

  opal entity <ID> <CREDENTIALS> [EXTRAS]

Arguments
---------

============= ===========
Argument      Description
============= ===========
``ID``	      Entity identifier.
============= ===========

Options
-------

===================================== ====================================
Option                                Description
===================================== ====================================
``--type TYPE, -ty TYPE``             Type of the entity (e.g. Participant, Instrument, Drug). Default type is Participant.
``--tables, -ta``                     To get the list of tables in which the entity with given id exists.
===================================== ====================================

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

Fetch the entities with id 1444:

.. code-block:: bash

  opal entity 1444 --opal https://opal-demo.obiba.org --user administrator --password password

Fetch the list of table where entity 1444 exists:

.. code-block:: bash

  opal entity 1444 --opal https://opal-demo.obiba.org --user administrator --password password --tables

Fetch the list of table where entity 1444 of type "Participant" exists:

.. code-block:: bash

  opal entity 1444 --opal https://opal-demo.obiba.org --user administrator --password password --tables --type Participant
