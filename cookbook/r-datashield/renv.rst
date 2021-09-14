.. _cb-renv:

How to Set up R/DataSHIELD Client Profiles
==========================================

Following the possibility to have different R/DataSHIELD server profiles (see :ref:`cb-r` and :ref:`cb-datashield-profiles`), it may be necessary to have different R environment on the client side as well. This is mandatory in the case of DataSHIELD where a server-side package only works with a specific client-side package version.

This concept of R environment is covered by the `renv R package <https://rstudio.github.io/renv/>`_ which intends to provide **isolated**, **portable** and **reproducible** R projects. Using ``renv`` gives full control of the user on its R exection environment, without depending on an IT infrastructure (different interfaces for different profiles).

In order to help with setting up such project, you can start with the `DSProjectTemplate <https://github.com/datashield/DSProjectTemplate>`_.

Add a Dependency on an R Package from GitHub
--------------------------------------------

As an example some of the DataSHIELD R packages are not available in the official CRAN repository. For R packages saved on `GitHub <https://github.com>`_ you can use the following procedure to include a new dependency:

.. note::

  1. Run ``renv::install()`` to retrieve a specific version of a R package from GitHub; for example ``renv::install("neelsoumya/dsSurvivalClient@v1.0.0")`` to install a released version of `dsSurvivalClient <https://github.com/neelsoumya/dsSurvivalClient>`_
  2. Edit your analysis script to make use of this package; for example ``library(dsSurvivalClient)``
  3. Run ``renv::snapshot()`` to register this package as part of your project environment

Remove a Dependency on an R Package
-----------------------------------

This is as simple as:

.. note::

  1. Edit your analysis script and remove the ``library()`` load statement of the package
  2. Run ``renv::snapshot()`` to unregister this package from your project environment
