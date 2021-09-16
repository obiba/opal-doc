How to Improve Performance
==========================

When it comes to importing data and performing analysis in the R server(s), the performance of the whole system setup (Opal, database, R server) must match the user needs. The performance will depend on:

* the volume of data and its dimensions (lot of records or lot of variables or both)
* the number of concurrent users
* the type of analyses that are conducted
* the type of hardware hosting the system (virtual vs. barebone, shared vs. dedicated)
* the version of the software

The following are recommendations and possible solutions (that can be combined) for improving the performance of your system.

Use Resources
-------------

If data are too large to be imported in the Opal's database, consider using the :ref:`intro-resources` as described in :ref:`cb-resources`. This will also save CPU and memory usage at data assignment time in R.

Increase Hardware Power
-----------------------

Extracting data from the database requires memory and CPU. Assigning data consumes the hardware resources for the Opal and R applications. Analysing data in R consumes CPU (one core per R session) and memory. When installed on the same server (not recommended), the database, Opal and R applications are then running concurrently which can lead to a freeze of the system (shared CPU cores, memory swapping).

The solution can be:

* Either to increase the host's hardware power (better and more CPUs, more memory),
* Or to isolate each application in its own server host. This can be done easily and dynamically for the R server (see :ref:`apps`).

Use Barebone Machine
--------------------

Cloud facilities offer the possibility to start Virtual Machines (VM), which is convenient but not optimal for intensive computations. Several VMs are running on a single hardware server, then sharing the access to the CPU cores and to the memory. Even when these hardware resources are reserved, there is still the virtualization extra layer that can affect the computation performance.

The solution can be to use barebone servers, i.e. dedicated servers that are accessed directly and not shared with others.

Do R Server Load Balancing
--------------------------

When many users are using the same R server simultaneously (R server can handle multiple R sessions in parallel), all the system's CPU cores may be in use. In addition to that the sytem's memory is shared among all the concurrent R sessions, which can break the R sessions running out of memory when one of them is too greedy.

The solution can be to increase the hardware resources (see previous section) or to add more R servers. Opal supports connection with multiple R servers, both for defining R/DataSHIELD profiles (see :ref:`cb-r`) and for balancing the computation load. To achieve that:

* Several R servers must belong to the same ``cluster``: see `Rock's Cluster Node Configuration <https://rockdoc.obiba.org/en/latest/admin/configuration.html#cluster-node-configuration>`_, corresponding to the `ROCK_CLUSTER Docker environment parameter <https://rockdoc.obiba.org/en/latest/admin/installation.html#docker-image-installation>`_.
* These R servers must run on different hosts

Opal will take in charge the creation of the R sessions in the way that it optimizes the usage of the cluster of R servers.

The advantage of this solution is that it does not require to modify the setup (database and Opal). Only new R servers will have to be declared in Opal and this can be done dynamically (service discovery or self-registration as documented in :ref:`apps`).

Keep Your Software Updated
--------------------------

New software version can bring new functionalities, and can also improve the operations performance. Unless stated in the release note and in the the release announcement, new versions of Opal are backward compatible. Make sure your IT department is keeping applications updated, which is also recommended for preventing security issues.

Save your R/DataSHIELD Workspace
--------------------------------

When conducting a R/DataSHIELD analysis, it can takes some computation time to get intermediate results. Instead of redoing the computations again and again at each R/DataSHIELD session, it is possible to save a snapshot of your R server session into a file that will be kept safe in Opal. The following R/DataSHIELD sessions can then reinstate at login time a previously saved workspace.

In the context of DataSHIELD, assign some data, make some preliminary computations and save R workspace:

.. code-block:: r

  library(DSOpal)
  library(dsBaseClient)
  builder <- DSI::newDSLoginBuilder()
  builder$append(server = "study1",
             user = "dsuser", password = "password",
             url = "https://opal-demo.obiba.org")
  builder$append(server = "study2",
             user = "dsuser", password = "password",
             url = "https://opal-demo.obiba.org")
  logindata <- builder$build()

  ##
  # start session: connect to the studies, no assignment
  ##
  conns <- datashield.login(logindata)

  # assign a table per study
  datashield.assign.table(conns, "cnsim", list(study1 = "CNSIM.CNSIM1", study2 = "CNSIM.CNSIM2"))
  # assign a resource and coerce to a data.frame
  datashield.assign.resource(conns, "cnsimClient", list(study1 = "RSRC.CNSIM1", study2 = "RSRC.CNSIM2"))
  datashield.assign.expr(conns, "cnsim.rsrc", quote(as.resource.data.frame(cnsimClient, strict = TRUE)))

  # get some summaries
  ds.summary("cnsim")
  ds.summary("cnsim.rsrc")

  # remove the resource client symbol
  ds.rm("cnsimClient")
  # verify symbols
  datashield.symbols(conns)

  # save remote R workspaces with a name
  datashield.workspace_save(conns, "assigned")

  # end session
  datashield.logout(conns)

Then in a next DataSHIELD, reinstate the saved R workspace:

.. code-block:: r

  library(DSOpal)
  library(dsBaseClient)
  builder <- DSI::newDSLoginBuilder()
  builder$append(server = "study1",
             user = "dsuser", password = "password",
             url = "https://opal-demo.obiba.org")
  builder$append(server = "study2",
             user = "dsuser", password = "password",
             url = "https://opal-demo.obiba.org")
  logindata <- builder$build()

  ##
  # start session: restore saved workspace
  ##
  conns <- datashield.login(logindata, restore = "assigned")

  # verify symbols
  datashield.symbols(conns)

  # get some summaries
  ds.summary("cnsim")
  ds.summary("cnsim.rsrc")

  # end session
  datashield.logout(conns)
