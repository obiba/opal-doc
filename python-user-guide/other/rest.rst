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
``--headers HEADERS, -hs HEADERS``                Custom headers in the form of: { "Key1": "Value1", "Key2": "Value2" }
================================================= ====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

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
