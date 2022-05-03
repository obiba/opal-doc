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

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

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
