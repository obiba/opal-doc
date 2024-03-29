Restore Project
===============

Restore the data of a project from a backup archive file to be found on the Opal file system. The destination project must exist and can have a name different from the original one (beware that this could break views). Default behavior is to stop when an item to restore already exist (override can be forced).

.. code-block:: bash

  opal restore-project <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
==================================================== =====================================
Option                                               Description
==================================================== =====================================
``--project PROJECT, -pr PROJECT``	                 Destination project name
``--archive ARCHIVE, -ar ARCHIVE``                   Archive directory or zip file path in the Opal file system
``--arpassword ARPASSWORD, -arp ARPASSWORD``         Password to decrypt zip archive (optional)
``--force, -f``                                      Force overwriting existing items (table, view, resource, report). Files override is not checked.
==================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Restore a project from the archive folder ``CNSIM`` into an existing project:

.. code-block:: bash

  opal restore-project --opal https://opal-demo.obiba.org --user administrator --password password --project datashield --archive /home/administrator/backup/CNSIM
