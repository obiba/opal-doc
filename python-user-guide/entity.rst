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

Fetch the entities with id 9553295965:

.. code-block:: bash

  opal entity 9553295965 --opal https://opal-demo.obiba.org --user administrator --password password

Fetch the list of table where entity 9553295965 exists:

.. code-block:: bash

  opal entity 9553295965 --opal https://opal-demo.obiba.org --user administrator --password password --tables

Fetch the list of table where entity 9553295965 of type "Participant" exists:

.. code-block:: bash

  opal entity 9553295965 --opal https://opal-demo.obiba.org --user administrator --password password --tables --type Participant
