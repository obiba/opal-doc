Data
====

Get data: list of entity identifiers or entity values from a table/variable.

.. code-block:: bash

  opal data <RESOURCE> <CREDENTIALS> [EXTRAS]

Arguments
---------

============= ===========
Argument      Description
============= ===========
``RESOURCE``	Resource identification in the format ``<datasource>.<table>[:<variable>]``. Each project has a datasource which is identified by the project's name.
============= ===========

.. include:: ../common-credentials.rst

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

Fetch the list of entity identifiers associated to a table:

.. code-block:: bash

  opal data CNSIM.CNSIM1 --opal https://opal-demo.obiba.org --user administrator --password password

Fetch the variable value for a entity in a table:

.. code-block:: bash

  # Get the JSON representation of all participant values in a table
  opal data CNSIM.CNSIM1 -o https://opal-demo.obiba.org -u administrator -p password --id 1444 -j

  # Get the JSON representation of a variable value
  opal data CNSIM.CNSIM1:GENDER -o https://opal-demo.obiba.org -u administrator -p password --id 1444 -j

  # Get the raw value. If variable is of binary type, a byte stream is outputed.
  opal data CNSIM.CNSIM1:GENDER -o https://opal-demo.obiba.org -u administrator -p password --id 1444 -j --raw
