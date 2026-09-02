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

.. _ds-quotas:

Quotas
------

A quota limits what a user may spend on DataSHIELD over a rolling time window. When the allowance is spent, Opal refuses to open **new** DataSHIELD sessions for that user; sessions that are already open are never interrupted, and keep working normally until they are closed or reach the inactivity timeout (see ``org.obiba.opal.r.sessionTimeout.DataSHIELD`` in :ref:`rconf`).

When no quota is defined, nothing is enforced and DataSHIELD usage is unlimited. This is the state of a freshly upgraded server: quotas only apply once an administrator has written one.

Metrics
~~~~~~~

A quota measures one of two things, and the choice says which resource is being protected:

* **Execution time**, the time the R server spent running the user's commands. It bills the CPU actually consumed and prices an idle session at zero. Choose it to bound how much computation a user may ask of the R servers.
* **Session time**, the wall-clock life of the user's R sessions, from creation to close, idle time included. An open DataSHIELD session is a live R process holding its memory whether or not it is computing, so this is what bounds how many R servers a user keeps alive and for how long. Choose it when memory pressure, rather than CPU, is the concern.

Neither subsumes the other: a user who runs one long computation and a user who leaves several idle sessions open cost the server differently. The two metrics are measured and enforced independently, so a subject can be given one quota of each, and a session is refused as soon as either is spent.

Note that a session always lasts at least as long as the commands it runs, so session time is always greater than or equal to execution time for the same sessions. Setting a session time limit below the execution time limit of the same subject makes the latter unreachable; the form warns when this happens.

Window
~~~~~~

The window is either the **last 24 hours** or the **last 7 days**, and it *rolls*: there is no reset instant and no period end. Usage is the sum over the sessions whose activity falls inside the window, so a user who runs out regains capacity progressively as old activity ages out, without any administrative action.

A user who is over an execution time quota is told when some capacity returns. A user who is over a session time quota because of sessions they still hold is told to close them instead: those sessions keep spending the allowance for as long as they are open, so waiting does not help.

Which quota applies
~~~~~~~~~~~~~~~~~~~

For each metric independently, Opal resolves the quota of a user in this order:

1. the user's own quota, if there is one;
2. otherwise the **most permissive** of the quotas of the groups the user belongs to — being added to a more generous group helps, it is never cancelled by a stricter one;
3. otherwise the system default;
4. otherwise no quota at all, i.e. unlimited.

Two consequences are worth knowing:

* A **disabled** quota is invisible to this resolution: the search falls through to the next level. Disabling is a way to park a quota, not a way to exempt its subject. To exempt one user from a system default, give them a personal quota with a limit high enough to be meaningless.
* A limit of **zero** is a valid quota: it forbids DataSHIELD altogether for that subject. "No quota configured" and "a quota of zero" are different things.

Limits are only ever compared within one metric, which is why a user can end up with an execution time quota from a group and a session time quota from the system default. Both then apply.

Administrators are not exempt: a quota is a statement about a principal. Opal's own internal R work is never accounted for and can never be blocked.

Operations
~~~~~~~~~~

Quotas are listed with the subject they apply to, their metric, their window, their limit and, for a personal quota, what that user has consumed so far.

Add Quota
^^^^^^^^^

A quota applies to everyone (the system default), to the members of a group, or to a single user. Pick the metric it limits, the window it is summed over, and the limit in minutes.

There can be only one quota per subject and metric: saving a second one for the same subject and metric replaces the first.

Edit Quota
^^^^^^^^^^

Any of the settings can be changed, including the subject and the metric. A change takes effect at the next session creation; nothing is cached and no session in progress is affected.

Delete Quota
^^^^^^^^^^^^

The subject becomes unlimited again for that metric, unless a broader quota (a group's, or the system default) still applies to them.

Consumption
~~~~~~~~~~~

What a user has consumed is visible on their subject profile page, alongside their R activity, where a personal quota can also be set directly. Users see their own consumption on their own profile page (see :ref:`my-profile`).

Audit
~~~~~

A refused session is written to the DataSHIELD user log with the numbers that caused it, so the reason a user was turned away can be read from the audit trail without correlating HTTP logs.

Permissions
-----------

Use Permission
~~~~~~~~~~~~~~

The use of the DataSHIELD service requires permission. This permission is to be combined with permissions on project tables and/or resources so that user can perform assignment operations in the R server.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Permission to install DataSHIELD R packages and to modify the global DataSHIELD configuration.
