.. _python-restore-project:

Restore Project
===============

Restore the data of a project from a backup archive file to be found on the Opal file system. The destination project must exist and can have a name different from the original one (beware that this could break views). Default behavior is to stop when an item to restore already exist (override can be forced). Note that a table or a view that is replaced loses its permissions, and the ones on its variables, whether ``--permissions`` is used or not.

The permissions found in the archive are restored only with the ``--permissions`` option. For each user or group and each item of the archive, the permissions of that user or group on that item are replaced by the archived ones; the permissions of other users and groups, and the ones on other items, are kept, with or without ``--force``. Only the permissions that apply to the destination project are restored, see :ref:`project-backup-restore` for details.

.. warning::

  A user or group name on another Opal server does not necessarily designate the same person. Check the users and groups of the archive before restoring permissions in another Opal than the one the archive comes from.

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
``--permissions``                                    Restore the project permissions found in the archive (default is false)
==================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Examples
--------

Restore a project from the archive folder ``CNSIM`` into an existing project:

.. code-block:: bash

  opal restore-project --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --archive /home/administrator/backup/CNSIM

Restore a project with its permissions, from the archive folder ``CNSIM``:

.. code-block:: bash

  opal restore-project --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --archive /home/administrator/backup/CNSIM --permissions
