User
====

Manage a user in the Opal internal user directory.

.. code-block:: bash

  opal user <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

============================================= =====================================
Option                                        Description
============================================= =====================================
``--name NAME, -n NAME``                      User name
``--fetch, -f``                               Fetch a user (all users are returned if no option --name is given)
``--delete, -de``                             Delete the user specified by the --name option
``--add, -a``                                 Add a user specified by the --name option
``--update, -ud``                             Update user password/certificate, status (enable/disable) and groups
``--upassword PWD, -upa PWD``                 User password of at least six characters.
``--ucertificate CERT, -uc CERT``             User certificate (public key) file
``--disabled, -di``                           Disable user account (if omitted the user is enabled by default).
``--groups GRP [GRP ...], -g GRP [GRP ...]``  User groups (separated by space)
============================================= =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Get the list of users with associated groups

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --fetch

Get a specific user with associated groups

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --fetch --name user1

Create the user user2

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --add --name user2 --upassword 123456

Create the user user3 with a certificate

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --ucertificate /path/to/certifcate.pem --add --name user3

Create the user (disabled) user4 with groups group1, group2 and group3

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --add --name user4 --disabled --upassword 123456 --groups  group1 group2 group3

Update user2's password

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --update --name user2 --upassword 987654

Update user2's status, set to disabled

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --update --name user2 --disabled

Update user2's status, set to enabled

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --update --name user2

Update user2's groups

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --update --name user2 --groups group1 group2

Delete the user user3

.. code-block:: bash

  opal user --opal https://opal-demo.obiba.org --user administrator --password password --delete --name user2
