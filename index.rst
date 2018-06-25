.. Opal documentation master file, created by
   sphinx-quickstart on Mon Apr  9 11:43:58 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

OBiBa Opal Documentation
=========================

Targeted at individual studies and study consortia, `OBiBa <http://obiba.org/>`_ software stack (Opal, Mica etc.) provides a software solution for epidemiological data management, analysis and publication. `Opal <http://www.obiba.org/pages/products/opal/>`_ is the core data warehouse application that provides all the necessary tools to import, transform and describe data. Opal can be used with `Agate <http://www.obiba.org/pages/products/agate/>`_, the `OBiBa <http://obiba.org/>`_'s central authentication server.

.. warning::

  Opal documentation is in the process of being rewritten. See also the :download:`Opal Documentation Archive <archive/OPALDOC.pdf>`

.. toctree::
   :maxdepth: 1

   introduction

.. toctree::
   :maxdepth: 1
   :caption: Administrator Guide

   admin/installation
   admin/configuration
   admin/plugins

.. toctree::
   :maxdepth: 1
   :caption: R Server Administrator Guide

   rserver-admin/installation
   rserver-admin/configuration

.. toctree::
   :maxdepth: 1
   :caption: Web User Guide

   web-user-guide/index

.. toctree::
   :maxdepth: 1
   :caption: Python User Guide

   python-user-guide/index
   python-user-guide/data-dictionary
   python-user-guide/data
   python-user-guide/entity
   python-user-guide/table-copy
   python-user-guide/table-delete
   python-user-guide/annot-export
   python-user-guide/annot-import
   python-user-guide/rest
