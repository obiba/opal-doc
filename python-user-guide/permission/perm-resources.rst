Resources Permission
====================

Manage permissions on a project's resources as a whole. These permissions apply to any resources in the project without needing to name them: after adding a resource the same permission will apply.

.. code-block:: bash

  opal perm-resources <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

===================================================== =====================================
Option                                                Description
===================================================== =====================================
``--add, -a``                                         Add a permission
``--delete, -d``                                      Delete a permission
``--permission PERM, -pe PERM``                       Permission to apply: ``view``, ``administrate``
``--subject SUBJECT, -s SUBJECT``                     Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``                             Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                    Project name on which the permission is to be set
===================================================== =====================================

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

Add view permission for subject demouser on any resource in RSRC project:

.. code-block:: bash

  opal perm-resources --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser  --permission view --add

Remove the above permission:

.. code-block:: bash

  opal perm-resource --opal https://opal-demo.obiba.org --user administrator --password password --type USER --project RSRC --subject demouser --delete
