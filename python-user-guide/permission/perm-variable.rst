Variable Permission
===================

Manage permissions on a project's variable (in a table).

.. code-block:: bash

  opal perm-variable <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

===================================================================== =====================================
Option                                                                Description
===================================================================== =====================================
``--add, -a``                                                         Add a permission
``--delete, -d``                                                      Delete a permission
``--permission PERM, -pe PERM``                                       Permission to apply: ``view``
``--subject SUBJECT, -s SUBJECT``                                     Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``                                             Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                                    Project name on which the permission is to be set
``--table TABLE, -t TABLE``                                           Table name to which the variables belong
``--variables VARIABLE [VARIABLE ...], -va VARIABLE [VARIABLE ...]``  List of variable names on which the permission is to be set
===================================================================== =====================================

.. include:: ../common-credentials.rst

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
``--json, -j``    Output pretty-print JSON
================= =================

Example
-------

Add view permission for subject demouser on variables GENDER and LAB_HDL of table CNSIM1 in datashield project:

.. code-block:: bash

  opal perm-variable --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --project datashield --table CNSIM1 --variables GENDER LAB_HDL --permission view  --add

Remove the above permission:

.. code-block:: bash

  opal perm-variable --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --project datashield --table CNSIM1 --variables GENDER LAB_HDL --delete
