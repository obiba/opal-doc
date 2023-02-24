Project Permission
==================

Manage global permissions on the project.

.. code-block:: bash

  opal perm-project <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--fetch, -f``                      Fetch permissions
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted (required on add/delete)
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``   Project name on which the permission is to be set
==================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add administrate permission for subject demouser on datashield project:

.. code-block:: bash

  opal perm-project --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission administrate --project datashield --add

Remove the above permission:

.. code-block:: bash

  opal perm-project --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --project datashield --delete
