Plugins
=======

Repository
----------

Opal plugins available are:

+----------------------------------------------------------------------+--------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| Name                                                                 | Type         | Description                                                                                        |  Depends                                                  | API                                                                                                               |
+======================================================================+==============+====================================================================================================+===========================================================+===================================================================================================================+
| `opal-search-es <https://github.com/obiba/opal-search-es/releases>`_ | opal-search  | | Opal search engine based on Elasticsearch 2.4. Can be used embedded in Opal (default) or         | No dependencies                                           | `Search Plugin API <https://github.com/obiba/opal/tree/master/opal-spi/src/main/java/org/obiba/opal/spi/search>`_ |
|                                                                      |              | | configured to connect to an Elasticsearch cluster.                                               |                                                           |                                                                                                                   |
+----------------------------------------------------------------------+--------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
| `jennite-vcf-store <https://github.com/obiba/jennite/releases>`_     | vcf-store    | | Stores the genotypes in Variant Call Format (VCF) files (binary flavor, BCF, is also supported). | | `htslib executables <http://www.htslib.org/download/>`_ | `VCF Store Plugin API <https://github.com/obiba/opal/tree/master/opal-spi/src/main/java/org/obiba/opal/spi/vcf>`_ |
|                                                                      |              | | VCF/BCF files can be downloaded filtered by participant phenotype criteria.                      | | (bcftools, tabix, bgzip)                                |                                                                                                                   |
+----------------------------------------------------------------------+--------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+


Installation
------------

All plugins are to be deployed as a directory at the following location: **OPAL_HOME/plugins**.

Automatic Installation
~~~~~~~~~~~~~~~~~~~~~~

Because having a search engine is an absolute requirement, Opal server will check at startup that there is a plugin of type ``opal-search`` and if it's not the case, the latest version of the `opal-search-es <https://github.com/obiba/opal-search-es/releases>`_ plugin (that applies to the current Opal server version) will be automatically downloaded and installed without needing a server restart. If for any reason this plugin cannot be automatically downloaded (network issue), the Opal start-up will fail and you will need to install the plugin manually.

Manual Installation
~~~~~~~~~~~~~~~~~~~

Available plugins can be downloaded from `OBiBa Plugins Repository <http://obiba.org/pages/plugins/>`_. The manual installation procedure should be performed as follow:

* Download the plugin of interest (zip file) from `OBiBa Plugins Repository <http://obiba.org/pages/plugins/>`_,
* Unzip plugin package in **OPAL_HOME/plugins** folder. Note that the plugin folder name does not matter, Opal will discover the plugin through the plugin.properties file that is expected to be found in the plugin folder.
* Read the installation instructions (if any) of the plugin to identify the system dependencies or any other information,
* Restart Opal.

Configuration
-------------

The OPAL_HOME/plugins folder contains all the Opal plugins that will be inspected at startup. A plugin is enabled if it has:

* A valid plugin.properties file,
* In case of several versions of the same plugin are installed, the latest one is selected.

The layout of the plugin folder is as follow:

.. code-block:: text

  OPAL_HOME/
  └── plugins
      └── <plugin-folder>
          ├── lib
          │   └── <plugin-lib>.jar
          ├── LICENSE.txt
          ├── README.md
          ├── plugin.properties
          └── site.properties


Inside the plugin's folder, a properties file, plugin.properties, has two sections:

* The required properties that describe the plugin (name, type, version etc.)
* Some default properties required at runtime (path to third-party executables for instance).

Still in the plugin's folder, a site-specific properties file, site.properties, is to be used for defining the local configuration of the plugin. Note that this file will be copied when upgrading the plugin.

Backups
-------

Opal assigns a data folder location to the plugin: **OPAL_HOME/data/<plugin-name>** where plugin-name is the name defined in the plugin.properties file. This folder is then the one to be backed-up.
