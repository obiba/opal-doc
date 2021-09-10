.. _cb-renv:

How to Set up R Client Profiles
===============================

Following the possibility to have different R/DataSHIELD server profiles (see :ref:`cb-r` and :ref:`cb-datashield-profiles`), it may be necessary to have different R denvironment on the client side as well. This is mandatory in the case of DataSHIELD where a server-side package only works with a specific client-side package version.

This concept of R environment is covered by the `renv R package <https://rstudio.github.io/renv/>`_ which intends to provide isolated, portable and reproducible R projects.
