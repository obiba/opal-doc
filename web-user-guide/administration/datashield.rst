DataSHIELD
==========

The `DataSHIELD platform <https://datashield.org>`_ configuration can be managed from this administration page. See the :ref:`rserver` documentation for understanding the underlying concepts of the integration of Opal with R.

Packages
--------

The DataSHIELD R packages management is done per R servers cluster.

The list of DataSHELD R packages (packages that declare some DataSHIELD configuration) is discovered by scanning the R packages installed on each R server of the cluster. This DataSHIELD configuration is expected to be either in the ``DESCRIPTION`` file or in a ``DATASHIELD`` file to be found in the package's installation directory. The items of this configuration are:

* **AggregateMethods** is a comma-separated list of key-value pairs, where the key is the R function name to be used on the R client-side and the value is the R function name that will be applied in the R server-side (if omitted, the server function name is assumed to be the same as the client function name within the R package namespace). These functions perform aggregation operation and return non-disclosive data.
* **AssignMethods** is a comma-separated list of key-value pairs, where the key is the R function name to be used on the R client-side and the value is the R function name that will be applied in the R server-side (if omitted, the server function name is assumed to be the same as the client function name within the R package namespace). These functions perform data assignment in the R server session and do not return values.
* **Options** is a comma-separated list of key-value pairs, where the key is the R option name and the value is the R option value, to be applied after the DataSHIELD R session creation.

Add Package
~~~~~~~~~~~

R packages are installed from the CRAN repositories defined in the Opal system which includes by default the `OBiBa CRAN <https://cran.obiba.org>`_ repository. See the Opal system configuration to modify this repository setting.

Adding "all DataSHIELD packages" means installing the `datashield <https://github.com/datashield/datashield>`_ R package which is a meta-package with dependencies.

Adding a specific DataSHIELD package will install the R package from the CRAN repositories or from a `GitHub <https://github.com>`_ repository.

When there are several R servers in the cluster, adding a R package will add it to all the R servers.

Delete all Packages
~~~~~~~~~~~~~~~~~~~

This will uninstall all the identified DataSHIELD R packages from the R server (as soon as their installation location is accessible!).

Remove Package
~~~~~~~~~~~~~~

This will uninstall the selected DataSHIELD R package from the R server (as soon as its installation location is accessible!).

When there are several R servers in the cluster, removing a R package will remove it from all the R servers.

Publish
~~~~~~~

Read the DataSHIELD configuration declared in the R package (as described above) and merge it in the corresponding DataSHIELD profile (the one with the same name as the considered R server cluster).

Unpublish
~~~~~~~~~

Read the DataSHIELD configuration declared in the R package (as described above) and removes it from the corresponding DataSHIELD profile (the one with the same name as the considered R server cluster).

Profiles
--------

A DataSHIELD profile is a combination of a R server profile (or cluster) with some specific settings. When end-user login in a DataSHIELD context and providing a profile name,
the R session will be created in the corresponding R server cluster and function call filtering will be applied based on the DataSHIELD profile settings.

Status
~~~~~~

A DataSHIELD profile can be disabled (recommended when modfying the settings). When disabled, no DataSHIELD R session can be created using this profile.

Permissions
~~~~~~~~~~~

By default a DataSHIELD profile can be used by any user with global DataSHIELD permission. It is also possible to restrict access to a profile by applying specific permissions. Note that granting permission to use a DataSHIELD profile also grants permission to use DataSHIELD generally.

Settings
~~~~~~~~

DataSHIELD settings control the R operations that can be performed in the DataSHIELD R session.

Initialization
^^^^^^^^^^^^^^

DataSHIELD settings can be initialized by selecting which DataSHIELD R packages methods and options are to be included in the allowed operations.

DataSHIELD methods are the function names that a DataSHIELD client is allowed to call. Each of these functions is mapped to a server-side function. This server-side function can be either a function name declared in its namespace (for instance ``base::ls`` or ``dsBase::colnamesDS``) or a custom R function script (for advanced users).

Aggregate Methods
^^^^^^^^^^^^^^^^^

The aggregation methods are used by DataSHIELD in order to compile individual data. The same aggregation methods must be defined in each DataSHIELD server that will be involved in a computation process. Each aggregation method is identified by a name that will be used from the R-DataSHIELD client.

Assign Methods
^^^^^^^^^^^^^^

The assign methods are used by DataSHIELD in order to transform individual data on server side. The same assign methods must be defined in each DataSHIELD server that will be involved in a computation process. Each assign method is identified by a name that will be used from the R-DataSHIELD client.

Options
^^^^^^^

The list of R options to apply after creating a DataSHIELD R session. These options are used to alter the behavior of the server-side functions (control of the privacy threshold for instance).

Permissions
-----------

Use Permission
~~~~~~~~~~~~~~

The use of the DataSHIELD service requires permission. This permission is to be combined with permissions on project tables and/or resources so that user can perform assignment operations in the R server.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Permission to install DataSHIELD R packages and to modify the global DataSHIELD configuration.
