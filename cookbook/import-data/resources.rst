How to NOT Import Data
======================

There are different reasons one would not import data into Opal:

* data are too large (timepoint series, genomes etc.)
* data are not tabular (linkage, multidimensional etc.)
* data cannot be extracted because they are linked to their computation environment (HPC, big data cluster etc.)
* data are already stored in a database that is kept updated
* data are not data (!) but computation services
* ...

Opal offers the alternative of using :ref:`intro-resources`, combined with the `resourcer R package <https://www.obiba.org/resourcer/>`_. See also the chapter `Orchestrating privacy-protected big data analyses of data from different resources with R and DataSHIELD: The Resources <https://isglobal-brge.github.io/resource_bookdown/resources.html>`_.

The general procedure is the following:

.. note::

  1. [optional] Design your own resource resolver/client in a R package, if the **resourcer** does not cover your needs, and make sure the R server(s) have this package installed
  2. Declare the resources in a Opal project and apply appropriate access permissions
  3. Use the resource from R/DataSHIELD in a R server

Step 1 - [optional] Design your Resource Resolver Package
---------------------------------------------------------

The `resourcer R package <https://www.obiba.org/resourcer/>`_ provides some of the most common resource resolvers (tidy files, databases and shell). Depending on the nature of your data and/or the location of these data, it may be necessary to design your own R package that extends the **resourcer** capabilities.

The `dsOmics R/DataSHIELD package <https://github.com/isglobal-brge/dsOmics>`_ is an example of an R/DataSHIELD package that provides its own resource Resolvers. More specifically, *dsOmics* uses the `Genomic Data Structure (GDS) <http://www.bioconductor.org/packages/release/bioc/html/gdsfmt.html>`_ file format for storing large, higly dimensional data on which computation can be done with a low memory footprint. It can also convert a Variant Call Format (VCF) file to a GDS one. As a reference, see the example code:

* `GDSFileResourceResolver.R <https://github.com/isglobal-brge/dsOmics/blob/master/R/GDSFileResourceResolver.R>`_ implements the GDS/VCF file resolver class,
* `GDSFileResourceClient.R <https://github.com/isglobal-brge/dsOmics/blob/master/R/GDSFileResourceClient.R>`_ implements the GDS/VCF file client that downloads the file and establishes a GDS connection object,
* `zzz.R <https://github.com/isglobal-brge/dsOmics/blob/master/R/zzz.R>`_ registers the package's specific resolvers on library load,
* `resource.js <https://github.com/isglobal-brge/dsOmics/blob/master/inst/resources/resource.js>`_ declares and documents the handled resources, so that Opal can discover them, generate corresponding resource creation forms, and load the R library before resource assignment in the R server.

Step 2 - Declare Resource in Opal
---------------------------------

If the resource access is protected by credentials, it is recommended that these credentials have data read-only permission and/or have limited allowed operations. For example, use :ref:`pat` to access a file stored in Opal, use a SQL view for a accessing a SQL database table etc.

From Project Page
~~~~~~~~~~~~~~~~~

.. note::

  1. Go to the project's page and select the **Resources** tab
  2. Press **Add Resource** and select the *Category* (nature of the resource) and the *Type* (service or data format and location) of the resource
  3. Fill in the connection form: *Parameters* and *Credentials*, and *Save*
  4. [optional] from the created resource page, press **Test** to try resource assignment in the **default** R server. This will check if the R resource resolver can be found, but will not establish a connection with the resource

Using R
~~~~~~~

A resource can be added to a project by a simple function call, assuming that you know how to express the URL to the resource:

.. code-block:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login(username = "administrator", password = 'password', url = 'https://opal-demo.obiba.org')

  # create an Opal file based resource
  opal.resource_create(o, "RSRC", "CNSIM3",
    url = "opal+https://opal-demo.obiba.org/ws/files/projects/RSRC/CNSIM3.zip",
    format = "csv", secret = "EeTtQGIob6haio5bx6FUfVvIGkeZJfGq")

  # to test the resource assignment and its resolution
  opal.assign.resource(o, "client", "RSRC.CNSIM3")
  opal.execute(o, "class(client)")

  opal.logout(o)

Step 3 - Use the Resources
--------------------------

Unlike working with an Opal table (which R assignment is straightforward), when using an Opal resource reference the data/services are made accessible after the following operations:

1. assign Opal's resource reference to the R server and make a resource Client object: this object does not establish the connection with the resource yet but has the appropriate code to do it
2. Either coerce the resource Client object to a ``data.frame`` (if the data have a tabular representation) and/or execute Client's specific data extraction/computation functions (e.g. execute a remote shell command or perform some computation on a specific data structure etc.).

For coercing to the tabular representation of a resource, use the `as.resource.data.frame() <file:///home/yannick/projects/resourcer/docs/reference/as.resource.data.frame.html>`_ function (that is DataSHIELD compatible) on the resource Client object.

Using R
~~~~~~~

See :ref:`r` documentation for setting up the R client.

.. code-block:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login(username = "administrator", password = 'password', url = 'https://opal-demo.obiba.org')

  # list resources in a project
  opal.resources(o, "RSRC")

  # assign a SQL database resource client
  opal.assign.resource(o, "client", "RSRC.CNSIM1")
  # coerce to a data.frame (tibble) and compute summary
  opal.assign.script(o, "data", quote(as.resource.data.frame(client)))
  opal.execute(o, "summary(data)")

  # assign a SSH resource client
  opal.assign.resource(o, "sshClient", "RSRC.brge_plink")
  # execute a shell command
  opal.execute(o, "sshClient$exec('ls')")

  opal.logout(o)

Using DataSHIELD
~~~~~~~~~~~~~~~~

Given the power of the resources, DataSHIELD is a better analysis environment for securing the access to the resource's data and capabilities. See :ref:`datashield` documentation.

.. code-block:: r

  library(DSOpal)
  library(dsBaseClient)
  builder <- DSI::newDSLoginBuilder()
  # connect to 'study1' on its 'default' profile
  builder$append(server = "study1",  url = "https://opal-demo.obiba.org",
             user = "dsuser", password = "password")
  logindata <- builder$build()
  conns <- DSI::datashield.login(logins = logindata)

  # list resources available
  datashield.resources(conns)

  # assign a resource client
  datashield.assign.resource(conns, "client", "RSRC.CNSIM1")
  # coerce to a (raw) data.frame and get summary
  datashield.assign.expr(conns, "data", quote(as.resource.data.frame(client, strict = TRUE)))
  ds.summary("data")

  datashield.logout(conns)
