My Profile
==========

Every user in Opal has a profile. This page is accessible by clicking on the user name on the top right corner of the web interface.

Account Settings
----------------

This section gives information about the user account: groups and how to change the password. As Opal is able to delegate the user authentication to tier systems (such as `Agate <http://agatedoc.obiba.org>`_ or :ref:`oidc`), Opal may have no control on the user's password. Unless the user has been defined in Opal (the *opal-user-realm*), the password update may be delegated to the original realm of the user.

Personal Access Tokens
----------------------

Personal access tokens can be created for use in scripts and on the command line (using R or Python client API). Be careful, these tokens are like passwords so you should guard
them carefully. The advantage to using a token over putting your password into a script is that a token can be revoked, and you can generate lots of them.

In addition to that, the scope of the access granted to the token can be restricted by projects, operations that can performed on these projects and system services. Note that this scope does not grant new permissions but rather alter the ones you have.

The personal access token is also the only way to authenticate in a script for users defined in a delegated :ref:`oidc`, as the process of authentication for such realms iplies the redirect of the user to a web page for manual login. The token is guaranteed to be safe for the Opal server as it is created by the user itself.

For these reasons, the personal API access token is the recommended way for authenticating within a Opal server (since Opal 2.15).

Example of usage in R (see section :ref:`r`):

.. code-block:: r

  o <- opal.login(token='dXvJKhk17RiO0TguRmR0EQlJxweCFyUX', url='https://opal-demo.obiba.org')
  ...

Example of usage in Python (see section :ref:`py`)

.. code-block:: python

  opal dict "datashield.*" --opal https://opal-demo.obiba.org --token 'dXvJKhk17RiO0TguRmR0EQlJxweCFyUX'

Example of usage with `cURL <https://curl.haxx.se/>`_ command line;

.. code-block:: bash

  curl -H "X-Opal-Auth: dXvJKhk17RiO0TguRmR0EQlJxweCFyUX" -H "Accept: application/json" -X GET https://opal-demo.obiba.org/ws/projects

Bookmarks
---------

Bookmarks are shortcuts to specific pages (project, table, variable) that can be selected by clicking on the start icon on the right of the title.
