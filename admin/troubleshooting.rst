.. _troubleshooting:

Troubleshooting
===============

This page covers problems that can prevent Opal from working, and how to recover from them.

Reporting an Issue
------------------

If you encounter an issue that you can't resolve, please report it in our `Opal Issue Tracker <https://github.com/obiba/opal/issues>`_.

Opal logs can be found in **/var/log/opal** for a package installation, and in **OPAL_HOME/logs** otherwise. Always refer to these logs when reporting an error.

.. _config-db-recovery:

Configuration Database Recovery
-------------------------------

When Opal keeps its configuration in the embedded H2 database (see :ref:`config-db`), the database file **OPAL_HOME/data/config/opal-config.mv.db** can be damaged by a power loss, a full disk or a storage failure while Opal writes to it. Opal then fails to start with an error about its configuration database, either ``File corrupted while reading record``, or ``Database may be already in use`` and ``The file is locked`` although no other process uses the file. H2 writes the underlying error to **OPAL_HOME/data/config/opal-config.trace.db**.

The content can usually be recovered with the tools of the H2 library that comes with Opal: the database is exported to SQL, then loaded into a new database file. The ``opal`` user is recreated with its original password, so that Opal opens the new database with the password it already has, which does not need to be known.

System Service
~~~~~~~~~~~~~~

In the commands below, ``OPAL_HOME`` is the Opal home directory and ``OPAL_DIST`` the Opal installation directory, the one that contains the ``lib`` directory. Run them as the user that runs Opal, so that the new files get the right owner.

#. Stop Opal, then back up the configuration database directory and the configuration file:

   .. code-block:: bash

     service opal stop
     cp -a $OPAL_HOME/data/config $OPAL_HOME/data/config.backup
     cp -a $OPAL_HOME/data/opal-config.xml $OPAL_HOME/data/opal-config.xml.backup

#. Export a copy of the database to SQL:

   .. code-block:: bash

     H2=$(ls $OPAL_DIST/lib/h2-*.jar)
     mkdir -p /tmp/opal-recovery/old /tmp/opal-recovery/new
     cp $OPAL_HOME/data/config/opal-config.mv.db /tmp/opal-recovery/old/
     cd /tmp/opal-recovery
     java -cp $H2 org.h2.tools.Recover -dir old -db opal-config

   This writes **old/opal-config.h2.sql**. Each part of the file that could not be read is reported in it by a ``// error`` line, and the rows it held are missing from the recovered configuration:

   .. code-block:: bash

     grep "// error" old/opal-config.h2.sql

#. Load the export into a new database, with a temporary user:

   .. code-block:: bash

     java -cp $H2 org.h2.tools.RunScript \
       -url "jdbc:h2:file:/tmp/opal-recovery/new/opal-config" \
       -user recovery -password recovery \
       -script old/opal-config.h2.sql

#. Check the content, then remove the temporary user:

   .. code-block:: bash

     java -cp $H2 org.h2.tools.Shell \
       -url "jdbc:h2:file:/tmp/opal-recovery/new/opal-config" -user recovery -password recovery \
       -sql "SHOW TABLES"
     java -cp $H2 org.h2.tools.Shell \
       -url "jdbc:h2:file:/tmp/opal-recovery/new/opal-config" -user recovery -password recovery \
       -sql "DROP USER recovery"

#. Replace the damaged database with the new one, and start Opal:

   .. code-block:: bash

     mkdir $OPAL_HOME/data/config.damaged
     mv $OPAL_HOME/data/config/opal-config.* $OPAL_HOME/data/config.damaged/
     cp /tmp/opal-recovery/new/opal-config.mv.db $OPAL_HOME/data/config/
     service opal start

Check in the Opal log that it starts, then that the projects, users and permissions are there. To go back, stop Opal and restore the backup of the first step. Keep the backup and the damaged files until the recovered configuration has been checked.

.. note::

  Use the H2 library of the Opal version that wrote the database: a database file is not always readable by another major version of H2.

Docker Service
~~~~~~~~~~~~~~

The `Opal Docker image <https://github.com/obiba/docker-opal>`_ does all of the above with one command, run with Opal stopped:

.. code-block:: bash

  docker compose stop opal
  docker compose run --rm --no-deps opal recover-config-db
  docker compose start opal

The command refuses to run while an Opal has the database open, in this container or in another one on the same volume. Nothing is deleted: the damaged files and the SQL export are moved to **data/config.damaged-<date>** in the Opal home volume. When parts of the file cannot be read, it lists them and changes nothing, as the rows they held would be missing from the recovered configuration. ``recover-config-db --force`` recovers what could be read anyway.

Then check that Opal starts, and that the projects, users and permissions are there.
