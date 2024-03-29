R
=

R servers can be managed from this administration page. A R server is a `Rock <https://rockdoc.obiba.org>`_ application.

R Servers
---------

The R servers are grouped by cluster. Each cluster can be administrated individually. See the :ref:`rserver` documentation for understanding the underlying concepts of the integration of Opal with R.

Status
~~~~~~

The R servers access can be tested, stopped and started. Stopping the R servers removes all the R sessions that could be in operation.

The output of the R commands that are executed on the R server are printed in the *Rserve.log* file that can be downloaded. This file is useful for troubleshooting (bad R command syntax, network failure, system dependency missing etc.).

Servers
~~~~~~~

Opal can connect to several R servers. All these servers are expected to be identical in terms of R base and packages versions. If this is not the case, this can be fixed by removing/installing packages: these operations apply to all the R servers in parallel.

Each R server can be started/stopped and log can be downloaded individually.

The R servers are provisioned as :ref:`apps` and therefore will be managed as such, i.e. either discovered or self-registered.

.. _r-packages:

Packages
~~~~~~~~

The list of all the R packages installed on the R server(s) side is available. Note that some of the packages are installed at a system level location (such as `/usr/local/lib/R/site-library`) whereas others are at a location that belongs to the `rserver` user (usually `/var/lib/rserver/R/library`). Only the latter can be edited, i.e. packages can be removed or installed. R uses an order for the package lookup and the user's one (`rserver`) comes before the system ones. Then it is valid to have the same package installed at different locations and with different versions.

The CRAN repositories that are referred when performing install or update package operations are the ones defined in the system configuration ``org.obiba.opal.r.repos`` (see :ref:`rconf`).

**Install single package**

Several installation methods are proposed:

* standard installation using the `install.package()` function based on the configured CRAN repositories.
* `remotes <https://www.rdocumentation.org/packages/remotes>`_ installation from a GitHub source repository, in which case the Git reference (commit number, tag or branch name) and the fully qualified package name (using the pattern `someUser/someRepo`) are mandatory.
* `Bioconductor <http://bioconductor.org>`_ manager installation.

**Update all packages**

This operation calls the `utils::update.packages() <https://www.rdocumentation.org/packages/utils/versions/3.6.2/topics/update.packages>`_ function to update all packages that can be updated to their latest version in the `rserver` R library location.

**Remove single package**

This will be effective if the package location is not a system one.

R Sessions
----------

Each user R session is created and managed by Opal, whether the context is plain R, DataSHIELD or report execution. The list of the R sessions reports who owns the R session, when was the last R command executed (Last access) and whether a R command is in progress (Status). When removing a R session, the remote R work directory is destroyed and all the associated R resources are freed.

R Workspaces
------------

Opal offers the possibility in the Opal R client API (see `opalr <https://www.rdocumentation.org/packages/>`_) to save the image of the remote R session into a file (within any files that could be found in the R session working directory) in a safe location on Opal server for latter reinstate. This service is available for DataSHIELD sessions too. The archived workspaces can be removed at any time.

Permissions
-----------

The use of the R service requires permission. Needless to say that it should be granted to trusted users only as the R scripting capabilities are potentially harmful for the hosting system (Opal data are safe though as a user could not transfer a Opal table to a R data.frame in the R server if s/he has no permission to see the values of this table).
