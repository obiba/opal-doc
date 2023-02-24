Resource Permission
===================

Manage permissions on a project's resource.

.. code-block:: bash

  opal perm-resource <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

=================================================================== =====================================
Option                                                              Description
=================================================================== =====================================
``--fetch, -f``                                                     Fetch permissions
``--add, -a``                                                       Add a permission
``--delete, -d``                                                    Delete a permission
``--permission PERM, -pe PERM``                                     Permission to apply: ``view``, ``administrate``
``--subject SUBJECT, -s SUBJECT``                                   Subject name to which the permission will be granted (required on add/delete)
``--type TYPE, -ty TYPE``                                           Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                                  Project name on which the permission is to be set
``--resources RESOURCE [RESOURCE ...], -r RESOURCE [RESOURCE ...]`` List of resource names on which the permission is to be get/set (default is all)
=================================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Add view permission for subject demouser on resource CNSIM1 in RSRC project:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser  --permission view --add --resources CNSIM1

Remove the above permission:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser --delete --resources CNSIM1

Add permission on all resources of RSRC project:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser --permission view --add

Remove permission from all resource of RSRC project:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser --delete

Add permission on specific resources:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser --permission view --add --resources CNSIM1 CNSIM2
