System Permission
=================

Manage global system permissions.

.. code-block:: bash

  opal perm-system <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``, ``add-project``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
==================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add add-project permission for subject demouser:

.. code-block:: bash

  opal perm-system --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission add-project --add

Remove the above permission:

.. code-block:: bash

  opal perm-system --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --delete
