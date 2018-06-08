.. Opal documentation master file, created by
   sphinx-quickstart on Mon Apr  9 11:43:58 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

OBiBa Opal Documentation
=========================

Targeted at individual studies and study consortia, `OBiBa <http://obiba.org/>`_ software stack (Opal, Mica etc.) provides a software solution for epidemiological data management, analysis and publication. While `Opal <http://www.obiba.org/pages/products/opal/>`_, the core data warehouse application, provides all the necessary tools to import, transform and describe data, `Mica <http://www.obiba.org/pages/products/mica/>`_ provides everything needed to build personalized web data portals and publish content of research activities of both studies and consortia. Based on the content defined in Mica, `Drupal <https://www.drupal.org/>`_ is the preferred platform to build your personalized web portal.
Mica is to be used with `Agate <http://www.obiba.org/pages/products/agate/>`_, the `OBiBa <http://obiba.org/>`_'s central authentication server which centralizes user related services such as profile management, and a notification system using emails.

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
   :caption: Web User Guide

   web-user-guide/index

.. toctree::
   :maxdepth: 1
   :caption: Python User Guide

   python-user-guide/index
   python-user-guide/rest
