Using DataSHIELD
================

Prerequisites
-------------

On client side, R is to be available. See the `R installation documentation <https://www.r-project.org/>`_ that matches your system.

Installation
------------

On Linux
~~~~~~~~

Installing the R packages requires the header files for the libcurl system library. To install this on ubuntu/debian (as root):

.. code-block:: bash

  sudo apt-get install libcurl4-openssl-dev

Then you can install the Opal package and its dependencies with this command within an R session:

.. code-block:: r

  install.packages('opal', repos=c('https://cran.rstudio.com/', 'https://cran.obiba.org'), dependencies=TRUE)

On Windows
~~~~~~~~~~

Installing the Opal R package on Windows requires that the package's dependencies be already installed:

.. code-block:: r

  install.packages(c('RCurl', 'rjson'), repos=c('https://cran.rstudio.com/', 'https://www.stats.ox.ac.uk/pub/RWin/'))

Once these are installed, the opal package can be installed like so:

.. code-block:: r

  install.packages('opal', repos='https://cran.obiba.org', type='source')

Usage
-----

Setting up User Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Using DataSHIELD requires two kind of permissions:

* 'Use' permission to DataSHIELD services: see DataSHIELD Permissions section for more details.
* At least 'View dictionary and summaries' permission to some data descriptions: see Table Permissions to know how to grant access to a table.

These access rights can be granted to a user or a group of users.

Deploying DataSHIELD packages in Opal
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each Opal must be configured the same way so that same computation is done in each Opal for one client request. This is done by relying on DataSHIELD-R packages repository.

See documentation about DataSHIELD Packages Administration. See also DataSHIELD documentation for Administrators.

In the following example, the *datashieldclient* package is to be installed.

DataSHIELD Usage
~~~~~~~~~~~~~~~~

First thing required to use DataSHIELD is to load datashieldclient, the DataSHIELD base package for the client, into your R environment:

.. code-block:: r

  # Install datashieldclient and dependecies if not already done
  install.packages('datashieldclient', repos=c(getOption('repos'), 'https://cran.obiba.org'), dependencies=TRUE)

  # Load datashieldclient library
  library(datashieldclient)

Create an Opal Object
~~~~~~~~~~~~~~~~~~~~~

Every method in the opal package has a required parameter of type 'opal'. This type of object can be obtained by calling the opal.login method. This is also th method used to authenticate with an Opal server.

.. code-block:: r

  # Create a Opal object
  o <- opal.login('username', 'password', 'https://opal.domain.org')

Alternatively, the url parameter can be specified as a list to login to multiple Opal instances with the same credentials (username/password) everywhere.

.. code-block:: r

  # Create a Opal object for each Opal url
  opals <- opal.login('username', 'password', list('https://opal.domain.org', 'https://opal.anotherdomain.org'))

This method returns an 'opal' (or a list thereof) object that can be passed to other methods later. The return value of this method should be stored in a variable for later use.

Finally, additional options can be specified using the opts parameter. This list is passed to the curlOptions method for setting HTTP options. Here are some useful ones:

================== =========================
Option             Description
================== =========================
``ssl.verifypeer`` Set to 0 to allow HTTPs connections to servers that provide self-signed certificates.
``ssl.verifyhost`` Set to 0 to allow HTTPs connections to servers that provides a certificate for a different hostname.
``sslversion``     Specify the SSL version number.
================== =========================

Invoking DataSHIELD Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~

As mentioned previously, all DataSHIELD methods require an argument of class 'opal' (returned by opal.login). This allows working with multiple opal instances in a single client:

.. code-block:: r

  # Login in each Opal
  studyA <- opal.login('username', 'password', 'https://opal.studya.org')
  studyB <- opal.login('username', 'password', 'https://opal.studyb.net')

  # Invoke some datashield methods
  datashield.assign(studyA, ...)
  datashield.assign(studyB, ...)

Since DataSHIELD is always using multiple Opal instances, the same methods are also able to work on a list of opal objects and will return a list of results.

.. code-block:: r

  # Login in each Opal
  studyA <- opal.login('username', 'password', 'https://opal.studya.org')
  studyB <- opal.login('username', 'password', 'https://opal.studyb.net')

  opals <- list(StudyA=studyA, StudyB=studyB)

  # Invoke a datashield method for all elements of 'opals'
  datashield.newSession(opals, ...)

This allows transforming for loops into single calls:

.. code-block:: r

  # Instead of this:
  for(k in opals) {
    datashield.assign(k, ...)
  }
  # Write this:
  datashield.assign(opals, ...)

Obviously, the downside is that the arguments are the same to all opal instances. If this is not the case, then a manual call to each opal instance will always be required.

Working with Server-Side R
~~~~~~~~~~~~~~~~~~~~~~~~~~

Assignments
^^^^^^^^^^^

Opal can push data into the server-side R environment and assigned to a particular symbol. This is done using the datashield.assign method. Opal can push a variable, a table (with all its variables) or even a datasource (with all tables and variables) into R and assign it to a R symbol. Opal data to be pushed are identified by Opal Fully Qualified Names.

.. code-block:: r

  # Assign the 'opal-data.Table:Variable' to the VAR symbol
  datashield.assign(opals, 'VAR', 'opal-data.Table:Variable')

  # Assign all variables from 'opal-data.Table' to the TBL symbol
  datashield.assign(opals, 'TBL', 'opal-data.Table')

  # Assign some enumerated variables from 'opal-data.Table' to the TBL symbol as a data.frame
  datashield.assign(opals, 'TBL', 'opal-data.Table', variables=list('VAR1','VAR2'))

  # Assign all continuous variables from 'opal-data.Table' to the TBL symbol as a data.frame
  datashield.assign(opals, 'TBL', 'opal-data.Table', variables='nature().any("CONTINOUS")')

The datashield.assign method can also be used to assign arbitrary R code on the server.

.. code-block:: r

  # Arbitrary R data can also be assigned on the server.
  # This requires the use of the quote() function to protect from local evaluation.
  datashield.assign(opals, 'some.data', quote(c(1:10)))
  datashield.assign(opals, 'other.data', quote(my.func(some.data)))

The remote R symbols can be listed and deleted.

.. code-block:: r

  # List the symbols in each Opal for the current datashield session
  datashield.symbols(opals)
  # Remove a symbol from each Opal for the current datashield session
  datashield.rm(opals, 'TBL')

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

  # Assign some Opal data in the environment
  datashield.assign(opals, 'BMI', 'opal-data.Impedence:BMI')

  # Use the 'length' aggregating method to retreive the length of the vector in each Opal
  datashield.length(opals, 'BMI')

  # Alternatively, use the 'aggregate' method to invoke 'length'
  # This form is used to invoke methods not defined by default
  datashield.aggregate(opals, 'length(BMI)')

Generalized Linear Model (glm) Example
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: r

  # Login to all Opal instances. The 'ssl.verifypeer' parameter is used to login to Opal instances that use self-signed certs.
  opals<-datashield.login('username', 'password', list(S1='https://demo.obiba.org:8443',
                                                     S2='https://opal.obiba.org',
                                                     S3='https://localhost:8080'), list(ssl.verifypeer=0))

  # Push the data we want to work with in the server-side R
  datashield.assign(opals, 'ds.demo', 'ds-demo.Simulated')

  # Optional step: convert the pairlist to a data.frame.  This step simplifies the call to datashield.glm
  datashield.assign(opals, 'ds.frame<-data.frame(as.list(ds.demo))')

  # Treat snp as factors (snp.f)
  datashield.assign(opals, 'snp.f<-as.factor(ds.frame$snp)')

  # Treat smoke as factors (smoke.f)
  datashield.assign(opals, 'smoke.f<-as.factor(ds.frame$smoke)')

  # Run glm. Note the usage of "quote()" to prevent early evaluation.
  datashield.glm(opals, CC~1+study.2+study.3+bmi+bmi.study.3+snp.f*smoke.f, quote(binomial))

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

DataSHIELD packages sources are hosted on GitHub.

Some DataSHIELD developers documentation is also available.
