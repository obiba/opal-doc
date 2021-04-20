.. _my-profile:

My Profile
==========

Every user in Opal has a profile. This page is accessible by clicking on the user name on the top right corner of the web interface.

Account Settings
----------------

This section gives information about the user account: groups and how to change the password. As Opal is able to delegate the user authentication to tier systems (such as `Agate <http://agatedoc.obiba.org>`_ or :ref:`oidc`), Opal may have no control on the user's password. Unless the user has been defined in Opal (the *opal-user-realm*), the password update may be delegated to the original realm of the user.

Personal Access Tokens
----------------------

Personal access tokens can be created for use in scripts and on the command line (using R or Python client API). Be careful, these tokens are like passwords so you should guard
them carefully. The advantage to using a token over putting your password into a script is that a token can be revoked, and you can generate lots of them. See also this `Personal Access Token <https://en.wikipedia.org/wiki/Personal_access_token>`_ page.

In addition to that, the scope of the access granted to the token can be restricted by projects, data access and operations that can be performed on these projects and system services. Note that **the personal access token does not grant new permissions** but rather alter the ones you have.

The personal access token is also the only way to authenticate in a script for users defined in delegated :ref:`oidc`, as the process of authentication for such realms implies the redirect of the user to a web page for manual login. The token is guaranteed to be safe for the Opal server as it is created by the user itself.

For these reasons, the personal API access token is the recommended way for authenticating within a Opal server (since Opal 2.15).

Projects
~~~~~~~~

The projects that are accessible using the token can be limited. When none is enumerated, all the projects accessible by the user will be accessible using the token.

Project Data
~~~~~~~~~~~~

The read/write operations can be controlled:

* **Default**, the user permissions apply,
* **Read only**, no data can be imported, nor modified/deleted. Individual-level data are still accessible.
* **Read only, without individual-level data**, no data can imported/exported, nor modified/deleted/extracted. Only reporting, analysis or DataSHIELD actions can be performed.

Project Tasks
~~~~~~~~~~~~~

This scope is for controlling which tasks can be launched on project:

* **Import**, import data (not available when project's data are read-only),
* **Export**, export data (not available when project's data are read-only without access to individual-level data),
* **Copy**, copy data (not available when project's data are read-only)
* **Backup**, backup project (not available when project's data are read-only without access to individual-level data),
* **Restore**, restore project (not available when project's data are read-only),
* **Report**, execute a report,
* **Analyse**, execute an analysis,
* **Import VCF**, import a VCF, when a VCF store plugin is installed (not available when project's data are read-only),
* **Export VCF**, export a VCF, when a VCF store plugin is installed (not available when project's data are read-only without access to individual-level data).

Project Administration
~~~~~~~~~~~~~~~~~~~~~~

This scope of operations is for managing projects:

* **Create**, to create new projects, not available when project access is restricted to some enumerated ones (otherwise created project would not be accessible),
* **Update**, to update a project settings (does not apply to project's data),
* **Delete**, to delete a project.

Services
~~~~~~~~

Along with project data, some system services can be used:

* **R**, which allows to create a plain R session in the R server backend, and assign some data (tables or resources), as soon as the user and token have permission to read individual-level data.
* **DataSHIELD**, which allows to create a DataSHIELD's R session in the R server backend, and assign some data (tables or resources), even when the user and token have not the permission to read individual-level data.
* **SQL**, which allows to make :ref:`sql` queries on tables, as soon as the user and token have permission to read individual-level data.
* **Administrate system**, which allows to manage plugins, DataSHIELD configuration and much more (*administrator* users only).

Examples
~~~~~~~~

Example of usage in R (see section :ref:`r`):

.. code-block:: r

  o <- opal.login(token='dXvJKhk17RiO0TguRmR0EQlJxweCFyUX', url='https://opal-demo.obiba.org')
  ...

Example of usage in Python (see section :ref:`py`)

.. code-block:: python

  opal dict "CNSIM.*" --opal https://opal-demo.obiba.org --token 'dXvJKhk17RiO0TguRmR0EQlJxweCFyUX'

Example of usage with `cURL <https://curl.haxx.se/>`_ command line;

.. code-block:: bash

  curl -H "X-Opal-Auth: dXvJKhk17RiO0TguRmR0EQlJxweCFyUX" -H "Accept: application/json" -X GET https://opal-demo.obiba.org/ws/projects



Bookmarks
---------

Bookmarks are shortcuts to specific pages (project, table, variable) that can be selected by clicking on the start icon on the right of the title.
