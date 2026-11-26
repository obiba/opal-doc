.. _project-backup-restore:

Project Backup and Restore
==========================

A project can be backed up into a folder of the Opal file system, and restored from that folder, or from a zip archive of it, into the same project or into another one. Both operations are launched from the **Backup / Restore** section of the project's **Administration** page, and run as tasks that can be followed in the task list.

The same operations are available from the command line, see the Python commands :ref:`backup-project <python-backup-project>` and :ref:`restore-project <python-restore-project>`.

Backup
------

The **Backup** action opens the **Backup Project** dialog, with the following options:

* **Backup Folder**, the folder of the Opal file system where the backup is written. It must not be inside the project's own folder.
* **Views as tables**, to export the data of the views instead of keeping their derivation scripts.
* **Backup permissions**, to include the project permissions in the backup (not checked by default).

The backup covers the tables (dictionary and data), the views (as logical or exported tables), the resources and the project files and, when asked, the permissions. It excludes the view change history, the table analyses, plugin-related data and other project elements.

Permissions in the backup
~~~~~~~~~~~~~~~~~~~~~~~~~

When **Backup permissions** is checked, the permissions granted to users and groups on the project are written in a ``permissions.json`` file at the root of the backup folder:

* the project permissions, and the permissions on its resources and on its VCF store,
* the permissions on the project's tables, views and variables.

Permissions on tables or variables that no longer exist are left out. When views are backed up as tables, their permissions are saved as table permissions.

.. note::

  The ``permissions.json`` file names the users and groups that have access to the project, and what they can do. Store and share the backup accordingly.

The permissions on the project files and folders, and the system permissions (administration, DataSHIELD, R etc.), are not part of the backup. See :doc:`../permissions` for the permissions that apply to a project.

Restore
-------

The destination project must exist, and can have a name different from the original one (beware that this could break views). The **Restore** action opens the **Restore Project** dialog, with the following options:

* **Backup Folder or Archive**, a backup folder, or a zip file of it, in the Opal file system.
* **Password**, to decrypt the zip archive, if it is encrypted.
* **Override existing items**, to replace the tables, views and resources that already exist in the project. Default behavior is to stop when an item to restore already exists. Note that a table or a view that is replaced loses its permissions, and the ones on its variables, whether **Restore permissions** is checked or not.
* **Restore permissions**, to grant again the project permissions found in the backup (not checked by default).

Permissions restore
~~~~~~~~~~~~~~~~~~~

The permissions are restored only when **Restore permissions** is checked, and when the backup has a ``permissions.json`` file (a backup made without permissions, or by an Opal version older than 6.3, has none and is restored without them).

.. warning::

  A user or group name on another Opal server does not necessarily designate the same person. Check the users and groups of the backup before restoring permissions in another Opal than the one the backup comes from.

The permissions are restored once the tables, views, resources and files are, as follows:

* They are applied to the destination project, whatever the name of the backed up one.
* For each user or group and each item of the backup, the permissions of that user or group on that item are replaced by the ones of the backup, as when setting a permission from the user interface. The permissions of other users and groups, and the ones on other items, are kept, whether **Override existing items** is checked or not.
* Only the project, resource, VCF store, table, view and variable permissions are restored, and only the ones that apply to each kind of item. Any other entry is skipped.
* Permissions on a table, view, variable or resource that is not in the restored project are skipped.

Users and groups are not created: a permission granted to a user or a group that is not known by Opal takes effect when it is.
