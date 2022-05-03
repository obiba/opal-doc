Table Delete
============

Delete one or more tables of a project.

.. code-block:: bash

  opal delete-table <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
===================== =====================================
Option                Description
===================== =====================================
``--project, -pr``	  Source project name
``--tables, -t``	    List of table names which will be deleted (default is all)
===================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras.rst

Example
-------

Delete some tables from a project:

.. code-block:: bash

  opal delete-table --opal https://opal-demo.obiba.org --user administrator --password password --project project_test --tables Table1 Table2

Delete all tables from a project:

.. code-block:: bash

  opal delete-table --opal https://opal-demo.obiba.org --user administrator --password password --project project_test
