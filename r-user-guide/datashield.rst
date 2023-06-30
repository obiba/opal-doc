.. _datashield:

Using DataSHIELD
================

Prerequisites
-------------

On client side, R is to be available. See the `R installation documentation <https://www.r-project.org/>`_ that matches your system.

Installation
------------

The Opal Client and DataSHIELD Interface R packages are available in the official CRAN:

* `opalr CRAN page <https://cran.r-project.org/package=opalr>`_
* `DSI CRAN page <https://cran.r-project.org/package=DSI>`_
* `DSOpal CRAN page <https://cran.r-project.org/package=DSOpal>`_
* `DSLite CRAN page <https://cran.r-project.org/package=DSLite>`_

You can install the DataSHIELD implementation for Opal R packages and dependencies with this command within an R session:

.. code-block:: r

  install.packages('DSOpal')

Usage
-----

Setting up User Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using DataSHIELD requires two kind of permissions:

* 'Use' permission to DataSHIELD services: see DataSHIELD Permissions section for more details.
* At least 'View dictionary and summaries' permission to some data descriptions: see Permissions section in :ref:`tables` and in :ref:`table` to know how to grant access to a table.

These access rights can be granted to a user or a group of users.

Deploying DataSHIELD packages in Opal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Opal must be configured the same way so that same computation is done in each Opal for one client request. This is done by relying on DataSHIELD-R packages repository.

See documentation about DataSHIELD Packages Administration. See also DataSHIELD documentation for Administrators.

DataSHIELD Usage
~~~~~~~~~~~~~~~~

First thing required to use DataSHIELD is to load datashieldclient, the DataSHIELD base package for the client, into your R environment:

.. code-block:: r

  # Install dsBaseClient and dependencies if not already done
  install.packages('dsBaseClient', repos=c(getOption('repos'), 'https://cran.obiba.org'))

  # Load DataSHIELD base package
  library(dsBaseClient)

Create a DATASHIELD Login Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every DataSHIELD operation requested on the analysis nodes require user authentication. The authentication credentials may be different in each of these server nodes. The first step is then build a DataSHIELD login data object that will group together the credentials and the connection details. The DSI package provides a utility R class to build this object.

.. code-block:: r

  # The login data object is a data.frame
  builder <- DSI::newDSLoginBuilder()
  builder$append(server="server1", url="https://opal.study1.org",
                 user="dsuser", password="password")
  builder$append(server="server2", url="https://opal.study2.org",
                 token="123456789")
  logindata <- builder$build()

  # Then perform login in each server
  library(DSOpal)
  connections <- datashield.login(logins=logindata)

Invoking DataSHIELD Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Every DataSHIELD functions defined in the `DSI <https://github.com/datashield/DSI>`_ package starts with `datashield.`. These functions allow to perform assignment and aggregation operations along with session management operations (workspaces, symbols, connection objects discovery etc.).

Working with Server-Side R
~~~~~~~~~~~~~~~~~~~~~~~~~~

The following is based on the DSI functions that are fully described in the `DSI README <https://github.com/datashield/DSI#higher-level-functions>`_.

Assignments
^^^^^^^^^^^

First operation is usually a data assignment, either by directly assigning the table as a `data.frame` object or by assigning a resource as a `ResourceClient` object (as defined in the `resourcer <https://github.com/obiba/resourcer>`_ package).

.. code-block:: r

  # assign Opal tables to symbol D
  datashield.assign.table(connections, symbol = "D",
                          table = list(server1 = "CNSIM.CNSIM1",
                                       server2 = "CNSIM.CNSIM2"))
  # assign Opal resources to symbol rsrc
  datashield.assign.resource(connections, symbol = "rsrc",
                             resource = list(server1 = "RSRC.CNSIM1",
                                             server2 = "RSRC.CNSIM2"))

It is possible to filter the variables of a table to be assigned:

.. code-block:: r

  # Assign some enumerated variables from 'opal-data.Table' to the TBL symbol as a data.frame
  datashield.assign.table(connections, symbol = "D",
                          table = list(server1 = "CNSIM.CNSIM1",
                                       server2 = "CNSIM.CNSIM2"),
                          variables=list('LAB_GLUC','LAB_HDL'))

The datashield.assign method can also be used to assign arbitrary R code on the server.

.. code-block:: r

  # Arbitrary R data can also be assigned on the server.
  # This requires the use of the quote() function to protect from local evaluation.
  datashield.assign(connections, 'some.data', quote(c(1:10)))
  datashield.assign(connections, 'other.data', quote(my.func(some.data)))

The remote R symbols can be listed and deleted.

.. code-block:: r

  # List the symbols in each Opal for the current datashield session
  datashield.symbols(connections)
  # Remove a symbol from each Opal for the current datashield session
  datashield.symbol_rm(connections, 'TBL')

Aggregations
^^^^^^^^^^^^

As per the DataSHIELD method, only aggregated data may be returned by the server. The server is configured with a set of methods provided to the DataSHIELD clients. The usage pattern is as follows:

* clients manipulate the server-side R environment (assign data, transform data, etc.)
* clients request an aggregate of some value in the R environment
* server extracts the requested value from the R environment
* server executes the aggregation method on the requested the data in a freshly created environment
* server returns aggregate data to clients.

This allows a broad range of possibilities to clients, but all "read" operations are controlled by the server and should not permit access to individual-level data.

The aggregation methods are defined by the server and so are configurable: see Aggregation Methods section in Opal Web Application User Guide to know how to manage these methods. But some should always be available since they are required to implement the DataSHIELD methods.

.. code-block:: r

  # Use the 'aggregate' method to invoke 'length'
  # This form is used to invoke methods not defined by default
  datashield.aggregate(connections, 'length(D$BMI)')

Extending DataSHIELD
--------------------

DataSHIELD is extensible; new aggregating methods can be defined on Opal servers such that any client can make use of them. It is also described here: Aggregation Methods section in Opal Web Application User Guide

DataSHIELD administrators can define two types of aggregating methods: R Function or R Script.

R Function Aggregating Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This type of aggregating method is used to directly invoke an R function on the data from the user's R environment. Because no pre-condition can be defined for these methods, they should be limited to very simple methods such as 'length'. Any R Function method can be written as an R Script method and may allow more control over what is being aggregated.

R Script Aggregating Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These types of aggregating methods are free-form R Scripts. They can invoke any R function available and also add pre and post conditions to what is being aggregated. Using this type of method requires more work for administrators, but allow more flexibility in terms of data security.

For example, pre conditions could validate that the input data has a minimum size before invoking a summarizing function on it. Post conditions could remove some unsafe data from the result before passing it back to clients.

Contributing to DataSHIELD Packages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DataSHIELD packages sources are hosted on GitHub. Some DataSHIELD developers documentation is also available. For more information visit the `DataSHIELD web site <https://datashield.org/>`_.
