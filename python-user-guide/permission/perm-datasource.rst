Datasource Permission
=====================

Manage permissions on the project's datasource (the set of tables).

.. code-block:: bash

  opal perm-datasource <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``, ``add-table``, ``view-value``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``   Project name on which the permission is to be set
==================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add add-table permission for subject demouser on datashield project:

.. code-block:: bash

  opal perm-datasource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission add-table --project datashield --add

Remove the above permission:

.. code-block:: bash

  opal perm-datasource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser  --project datashield --delete
