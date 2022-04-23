Backup Project
==============

The project backup task has a limited scope: tables (dictionary and data export), views (either as a logical table or as an exported table), resources, files and report templates. Other project elements that are not part of the backup: user and group permissions, view change history, table analysis, report executions etc.

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
==================================================== =====================================

.. include:: ../common-credentials.rst

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
================= =================

Example
-------

Backup a specific project from a project, wait for the task to complete and download the archive as an encrypted zip file:

.. code-block:: bash

  opal backup-project --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --archive /home/administrator/backup/CNSIM | opal task --opal https://opal-demo.obiba.org --user administrator --password password --wait && opal file --opal https://opal-demo.obiba.org --user administrator --password password --download-password foobar123 /home/administrator/backup/CNSIM > CNSIM.zip
