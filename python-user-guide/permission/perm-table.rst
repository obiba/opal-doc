Table Permission
================

Manage permissions on a project's table.

.. code-block:: bash

  opal perm-table <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

===================================================== =====================================
Option                                                Description
===================================================== =====================================
``--fetch, -f``                                       Fetch permissions
``--add, -a``                                         Add a permission
``--delete, -d``                                      Delete a permission
``--permission PERM, -pe PERM``                       Permission to apply: ``view``, ``view-value``, ``edit``, ``edit-values``, ``administrate``
``--subject SUBJECT, -s SUBJECT``                     Subject name to which the permission will be granted (required on add/delete)
``--type TYPE, -ty TYPE``                             Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                    Project name on which the permission is to be set
``--tables TABLE [TABLE ...], -t TABLE [TABLE ...]``  List of table names on which the permission is to be get/set (default is all)
===================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add view permission for subject demouser on table CNSIM1 in CNSIM project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project CNSIM --subject demouser  --permission view --add --tables CNSIM1

Remove the above permission:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project CNSIM --subject demouser --delete --tables CNSIM1

Add permission on all tables of CNSIM project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project CNSIM --subject demouser --permission view --add

Remove permission from all table of CNSIM project:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project CNSIM --subject demouser --delete

Add permission on specific tables:

.. code-block:: bash

  opal perm-table --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project CNSIM --subject demouser --permission view --add --tables CNSIM1 --tables FNAC