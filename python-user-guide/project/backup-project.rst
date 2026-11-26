.. _python-backup-project:

Backup Project
==============

The project backup task has a limited scope: tables (dictionary and data export), views (either as a logical table or as an exported table), resources, files, report templates and, optionally, user and group permissions. Other project elements that are not part of the backup: view change history and tags, table analysis, report executions etc.

The permissions are backed up only with the ``--permissions`` option, in a ``permissions.json`` file of the archive. It holds the permissions on the project, its resources, VCF store, tables, views and variables; the permissions on the project files and folders, and the system permissions, are not included. See :ref:`project-backup-restore` for details.

.. code-block:: bash

  opal backup-project <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
==================================================== =====================================
Option                                               Description
==================================================== =====================================
``--project PROJECT, -pr PROJECT``                   Source project name
``--archive ARCHIVE, -ar ARCHIVE``                   Archive directory path in the Opal file system
``--views-as-tables, -vt``                           Treat views as tables, i.e. export data instead of keeping derivation scripts (default is false)
``--force, -f``                                      Force overwriting an existing backup folder
``--permissions``                                    Backup the project permissions (default is false)
==================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Examples
--------

Backup a specific project from a project, wait for the task to complete and download the archive as an encrypted zip file:

.. code-block:: bash

  opal backup-project --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --archive /home/administrator/backup/CNSIM | opal task --opal https://opal-demo.obiba.org --user administrator --password password --wait && opal file --download --opal https://opal-demo.obiba.org --user administrator --password password --download-password foobar123 /home/administrator/backup/CNSIM > CNSIM.zip

Backup a project with its permissions:

.. code-block:: bash

  opal backup-project --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --archive /home/administrator/backup/CNSIM --permissions
