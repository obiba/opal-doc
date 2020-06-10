DataSHIELD
==========

The DataSHIELD configuration can be managed from this administration page.

Packages
--------

The list of DataSHELD R packages is discovered by scanning the R packages installed on the R server that declare some DataSHIELD configuration. This DataSHIELD configuration is expected to be either in the ``DESCRIPTION`` file or in a ``DATASHIELD`` file to be found in the package's installation directory. The items of this configuration are:

* **AggregateMethods** is a comma-separated list of key-value pairs, where the key is the R function name to be used on the R client-side and the value is the R function name that will be applied in the R server-side (if omitted, the server function name is assumed to be the same as the client function name within the R package namespace). These functions perform aggregation operation and return non-disclosive data.
* **AssignMethods** is a comma-separated list of key-value pairs, where the key is the R function name to be used on the R client-side and the value is the R function name that will be applied in the R server-side (if omitted, the server function name is assumed to be the same as the client function name within the R package namespace). These functions perform data assignment in the R server session and do not return values.
* **Options** is a comma-separated list of key-value pairs, where the key is the R option name and the value is the R option value, to be applied after the DataSHIELD R session creation.

Add Package
~~~~~~~~~~~

R packages are installed from the CRAN repositories defined in the Opal system which includes by default the `OBiBa CRAN <https://cran.obiba.org>`_ repository. See the Opal system configuration to modify this repository setting.

Adding "all DataSHIELD packages" means installing the `datashield <https://github.com/datashield/datashield>`_ R package which is a meta-package with dependencies.

Adding a specific DataSHIELD package will install the R package from the CRAN repositories or from a `GitHub <https://github.com>`_ repository.

Delete all Packages
~~~~~~~~~~~~~~~~~~~

This will uninstall all the identified DataSHIELD R packages from the R server (as soon as their installation location is accessible!).

Remove Package
~~~~~~~~~~~~~~

This will uninstall the selected DataSHIELD R package from the R server (as soon as its installation location is accessible!).

Publish Methods
~~~~~~~~~~~~~~~

Read the DataSHIELD configuration declared in the R package (as described above) and merge it in the Opal's global DataSHIELD configuration.

Options
-------

The list of R options to apply after creating a DataSHIELD R session.

Add R Option
~~~~~~~~~~~~

Provide the option key-value pair.

Methods
-------

DataSHIELD methods are the function names that a DataSHIELD client is allowed to call. Each of these functions is mapped to a server-side function. This server-side function can be either a function name declared in its namespace (for instance ``base::ls`` or ``dsBase::colnamesDS``) or a custom R function script (for advanced users).

Aggregate Methods
~~~~~~~~~~~~~~~~~

The aggregation methods are used by DataSHIELD in order to compile individual data. The same aggregation methods must be defined in each DataSHIELD server that will be involved in a computation process. Each aggregation method is identified by a name that will be used from the R-DataSHIELD client.

Assign Methods
~~~~~~~~~~~~~~

The assign methods are used by DataSHIELD in order to transform individual data on server side. The same assign methods must be defined in each DataSHIELD server that will be involved in a computation process. Each assign method is identified by a name that will be used from the R-DataSHIELD client.

Permissions
-----------

Use Permission
~~~~~~~~~~~~~~

The use of the DataSHIELD service requires permission. This permission is to be combined with permissions on project tables and/or resources so that user can perform assignment operations in the R server.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Permission to install DataSHIELD R packages and to modify the global DataSHIELD configuration.
