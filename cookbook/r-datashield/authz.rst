How to Manage Authentication and Authorizations
===============================================

Apply DataSHIELD Permissions
----------------------------

It is recommended to grant permissions by group, and then assign each user to the appropriate groups.

There are two kinds of permissions that need to be granted:

* Permission to use the DataSHIELD service, defined globally
* Permission to use data (table or resource) in the context of DataSHIELD, defined per table of per resource

Note that the DataSHIELD-compatible permissions (view dictionary and summary, without individual values access) are to be applied per table, whereas it is possible to apply similar permission (view, without resource credentials access) to any resource of a project in a single operation.

From Web Page
~~~~~~~~~~~~~

.. note::

  As a system administrator:

  1. [optional] Group local users (if not already done): go to **Administration > Users and Groups** and edit users so that they belong to the relevant group
  2. [optional] Configure :ref:`oidc` so that the users are automatically granted the appropriate group: go to **Administration > Identity Providers** and configure each ID provider (groups can be automatically applied or extracted from the received UserInfo).
  3. Grant group the permission to *use* the DataSHIELD service: go to **Administration > DataSHIELD**, *Permissions* section (bottom of the page)

  As a system administrator or as a project administrator:

  * Grant group the permission to *view dictionnary and summary (no access to individual values)* of a Table: go to project's table page, select the **Permissions** tab
  * Grant group the permission to *view (no credentials)* a Resource: go to the project's resource page, select the **Permissions** tab
  * Grant group the permission to *view (no credentials)* any Resources of a project: go to the project's resources list page, select the **Permissions** tab

Using R
~~~~~~~

Use the following *opalr* R functions to manage permissions:

* Table permissions functions ``opal.table_perm*`` (`opal.table_perm_add() <https://www.obiba.org/opalr/reference/opal.table_perm_add.html>`_ etc.)
* Resource permissions functions ``opal.resource_perm`` (`opal.resource_perm_add() <https://www.obiba.org/opalr/reference/opal.resource_perm_add.html>`_ etc.) and ``opal.resources_perm`` (`opal.resources_perm_add() <https://www.obiba.org/opalr/reference/opal.resources_perm_add.html>`_ etc.)

The following example grants DataSHIELD permissions to ``projectA`` and ``projectB`` groups:

.. code-block:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login(username = "administrator", password = 'password', url = 'https://opal-demo.obiba.org')

  # create a user in a group, call output is the generated password
  pwd <- oadmin.user_add(o, "foo", groups = c("projectA"))

  # use DataSHIELD service
  dsadmin.perm_add(o, subject = c("projectA", "projectB"), type = "group", permission = "use")

  # single table
  opal.table_perm_add(o, 'CNSIM', 'CNSIM1', c('projectA', 'projectB'), type = 'group', permission = 'view')

  # each table of a project
  lapply(opal.tables(o, "CNSIM")$name, function(table) {
    opal.table_perm_add(o, "CNSIM", table, subject = c("projectA", "projectB"), type = "group", permission = "view")
  })

  # single resource
  opal.resource_perm_add(o, "RSRC", "CNSIM1", subject = c("projectA", "projectB"), type = "group", permission = "view")

  # any resources of a project
  opal.resources_perm_add(o, "RSRC", subject = c("projectA", "projectB"), type = "group", permission = "view")

  opal.lgout(o)

Use Personal Access Token
-------------------------

As documented in the :ref:`pat` documentation, the PAT is the recommended authentication strategy, as it has a limited scope (project access and operations), and is revocable. Its usage is mandatory when the user is authenticated externally (see :ref:`oidc` documentation).

Create a PAT
~~~~~~~~~~~~

.. rubric:: From Profile Page

.. note::

  1. Go to **My Profile** page (press the username on the top right corner)
  2. Press **Add Access Token** and select a prepared token configuration (*DataSHIELD*, etc.) or a custom one
  3. Fill in the token form
  4. Copy the generated token and *Save*

.. rubric:: Using R

Use the ``opal.token*`` functions to manage your PATs. More specifically, use the prepared token configurations `opal.token_r_create() <https://www.obiba.org/opalr/reference/opal.token_r_create.html>`_, `opal.token_datashield_create() <https://www.obiba.org/opalr/reference/opal.token_datashield_create.html>`_, or `opal.token_sql_create() <https://www.obiba.org/opalr/reference/opal.token_sql_create.html>`_.

.. code:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login()

  # the output of the call is the token
  token <- opal.token_datashield_create(o, "test")

  opal.logout(o)

Use the PAT
~~~~~~~~~~~

Replace in your R/DataSHIELD, or Python, scripts the username/password credentials by the `token` parameter.

.. rubric:: In R

.. code:: r

  # load opal library
  library(opalr)
  # connect to the opal server with a token
  o <- opal.login(token = "xxxxxxx", url = "https://opal.example.org")

  # ...

.. rubric:: In DataSHIELD

.. code:: r

  library(DSOpal)
  library(dsBaseClient)
  builder <- DSI::newDSLoginBuilder()
  # connect to 'study1' with a token
  builder$append(server = "study1",  url = "https://opal-demo.obiba.org",
                 token = "xxxxxxxx")
  logindata <- builder$build()
  conns <- DSI::datashield.login(logins = logindata)

  # ...

DataSHIELD and Central Authentication Service
---------------------------------------------

In the DataSHIELD context, managing users is usually a pain for the infrastructure coordinator as each data node custodian must create a user, which takes time, and with potentially as many different passwords to keep safe.

An different setup is to use a Central Authentication Service (CAS), where users are registered once and properly configured (profiles/groups). Then each DataSHIELD Opal would connect to the CAS. Opal supports external :ref:`oidc` using the standard `OpenID Connect protocol <https://openid.net/connect/>`_.

The `opalr` R package does not currently support the OpenID dance (and it is anyway not appropriate for a scripting usage), then a user must login the Opal web interface of each node once, so that its user profile is validated and to create :ref:`pat` that will be used in its DataSHIELD R scripts.
