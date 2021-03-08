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
``--add, -a``                                                       Add a permission
``--delete, -d``                                                    Delete a permission
``--permission PERM, -pe PERM``                                     Permission to apply: ``view``, ``administrate``
``--subject SUBJECT, -s SUBJECT``                                   Subject name to which the permission will be granted
``--type TYPE, -ty TYPE``                                           Subject type: ``user`` or ``group``
``--project PROJECT, -pr PROJECT``                                  Project name on which the permission is to be set
``--resources RESOURCE [RESOURCE ...], -r RESOURCE [RESOURCE ...]`` List of resource names on which the permission is to be set (default is all)
=================================================================== =====================================

Credentials
-----------

Authentication can be done by username/password credentials OR by personal access token OR by certificate/private key pair (two-way SSL authentication).

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url
``--user USER, -u USER``              Credentials auth: user name (requires a password)
``--password PASSWORD, -p PASSWORD``  Credentials auth: user password (requires a user name)
``--token TOKEN, -tk TOKEN``          Token auth: User access token
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Two-way SSL auth: certificate/public key file (requires a private key)
``--ssl-key SSL_KEY, -sk SSL_KEY``    Two-way SSL auth: private key file (requires a certificate)
===================================== ====================================

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
