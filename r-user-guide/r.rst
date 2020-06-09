.. _r:

Using R
=======

Prerequisites
-------------

On client side, R is to be available. See the `R installation documentation <https://www.r-project.org/>`_ that matches your system.

Installation
------------

The Opal Client R package is available in the official CRAN: see `opalr CRAN page <https://cran.r-project.org/package=opalr>`_

You can install the Opal package and its dependencies with this command within an R session:

.. code-block:: r

  install.packages('opalr', dependencies=TRUE)

Usage
-----

Accessing Opal data using R is straightforward:

.. code-block:: r

  # load opal library
  library(opalr)

  # get a reference to the opal server
  o <- opal.login('administrator','password','https://opal-demo.obiba.org')

  # assign some data to a data.frame
  opal.assign.table(o,'CNSIM1','CNSIM.CNSIM1',variables=list('GENDER','PM_BMI_CONTINUOUS'))

  # do some analysis on the remote R session
  opal.execute(o,'summary(CNSIM1)')

  # get the remote data.frame on the client
  D <- opal.execute(o,'CNSIM1')
  head(D)

  # or send a R script to the R server and execute it
  rval <- opal.execute.source(o, '/path/to/script.R')

  # clean remote R session
  opal.logout(o)

See also `Opal R example scripts <https://github.com/obiba/opalr/tree/master/inst/examples>`_.

Security
--------

As the user is authenticated against Opal, the authorizations granted to this user applies. If user is only allowed to access to the variables and not the data, the data assignment to R will fail.

In addition to the data and variables related permissions, the user must have been granted the permission to use the R service.

It is highly recommended to access to a Opal server through the secured protocol HTTPS (Opal address starting with https://).

Advanced users can login to Opal by providing a key pair: certificate and private key. Example:

.. code-block:: r

  credentials <- list(
    sslcert='my-publickey.pem',
    sslkey='my-privatekey.pem')

  o <- opal.login(url='https://opal-demo.obiba.org', opts=credentials)

Probably the most secure authentication method is by using a personal access token (since Opal 2.15).

.. code-block:: r

  o <- opal.login(token='dXvJKhk17RiO0TguRmR0EQlJxweCFyUX', url='https://opal-demo.obiba.org')
