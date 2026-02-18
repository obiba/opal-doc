Restore Views
=============

Restore views that were previously backed up in the local file system into a project. The expected format of the
view files is JSON. If one or more tables that are referenced by the backed up view do not exist anymore, the restoration will fail.

.. code-block:: bash

  opal restore-view <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
==================================================== =====================================
Option                                               Description
==================================================== =====================================
``--project PROJECT, -pr PROJECT``	                 Destination project name
``--views VIEWS [VIEWS ...], -vw VIEWS [VIEWS ...]`` List of view names to be restored (default is all the JSON files that are found in the backup directory)
``--input INPUT, -in INPUT``                         Input directory name (default is current directory)
``--force, -f``                                      Skip confirmation when overwriting an existing view.
==================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras.rst

Example
-------

Restore a specific view file ``CNSIM.json`` into a project:

.. code-block:: bash

  opal restore-view --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --views CNSIM
