Variable Permission
===================

Manage permissions on a project's variable (in a table).

.. code-block:: bash

  opal perm-variable <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

======================================================================================== =====================================
Option                                                                                   Description
======================================================================================== =====================================
``--fetch, -f``                                                                          Fetch permissions
``--add, -a``                                                                            Add a permission
``--delete, -d``                                                                         Delete a permission
``--permission PERM, -pe PERM``                                                          Permission to apply: ``view``
``--subject SUBJECT, -s SUBJECT``                                                        Subject name to which the permission will be granted (required on add/delete)
``--type TYPE, -ty TYPE``                                                                Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                                                       Project name on which the permission is to be set
``--table TABLE, -t TABLE``                                                              Table name to which the variables belong
``--variables VARIABLE1 [--variables VARIABLE2 ...], -va VARIABLE1 [-va VARIABLE2 ...]`` List of variable names on which the permission is to be get/set (default is all)
======================================================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add view permission for subject demouser on variables GENDER and LAB_HDL of table CNSIM1 in CNSIM project:

.. code-block:: bash

  opal perm-variable --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --project CNSIM --table CNSIM1 --variables GENDER --variables LAB_HDL --permission view  --add

Remove the above permission:

.. code-block:: bash

  opal perm-variable --opal https://opal-demo.obiba.org --user administrator --password password --type USER --subject demouser --project CNSIM --table CNSIM1 --variables GENDER --variables LAB_HDL --delete