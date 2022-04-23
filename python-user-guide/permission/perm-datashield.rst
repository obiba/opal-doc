DataSHIELD Permission
=====================

Manage DataSHIELD usage permissions.

.. code-block:: bash

  opal perm-datashield <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

==================================== =====================================
Option                               Description
==================================== =====================================
``--add, -a``                        Add a permission
``--delete, -d``                     Delete a permission
``--permission PERM, -pe PERM``      Permission to apply: ``administrate``, ``use``
``--subject SUBJECT, -s SUBJECT``    Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``            Subject type: ``user`` or ``group``
==================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add use permission for subject demouser:

.. code-block:: bash

  opal perm-datashield --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --permission use --add

Remove the above permission:

.. code-block:: bash

  opal perm-datashield --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --delete
