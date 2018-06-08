Plugins
=======

Repository
----------

Mica plugins available are:

==================================================================== =========== =========================================================================================================================================== =============== ============
Name                                                                 Type        Description                                                                                                                                 Depends         API
==================================================================== =========== =========================================================================================================================================== =============== ============
`mica-search-es <https://github.com/obiba/mica-search-es/releases>`_ mica-search Mica search engine based on Elasticsearch 2.4. Can be used embedded in Mica (default) or configured to connect to an Elasticsearch cluster. No dependencies `Search Plugin API <https://github.com/obiba/mica2/tree/master/mica-spi/src/main/java/org/obiba/mica/spi/search>`_
==================================================================== =========== =========================================================================================================================================== =============== ============

Installation
------------

All plugins are to be deployed as a directory at the following location: **MICA_HOME/plugins**.

Automatic Installation
~~~~~~~~~~~~~~~~~~~~~~

Because having a search engine is an absolute requirement, Mica server will check at startup that there is a plugin of type ``mica-search`` and if it's not the case, the latest version of the `mica-search-es <https://github.com/obiba/mica-search-es/releases>`_ plugin (that applies to the current Mica server version) will be automatically downloaded and installed without needing a server restart. If for any reason this plugin cannot be automatically downloaded (network issue), the Mica start-up will fail and you will need to install the plugin manually.

Manual Installation
~~~~~~~~~~~~~~~~~~~

Available plugins can be downloaded from `OBiBa Plugins Repository <http://obiba.org/pages/plugins/>`_. The manual installation procedure should be performed as follow:

* Download the plugin of interest (zip file) from `OBiBa Plugins Repository <http://obiba.org/pages/plugins/>`_,
* Unzip plugin package in **MICA_HOME/plugins** folder. Note that the plugin folder name does not matter, Mica will discover the plugin through the plugin.properties file that is expected to be found in the plugin folder.
* Read the installation instructions (if any) of the plugin to identify the system dependencies or any other information,
* Restart Mica.

Configuration
-------------

The MICA_HOME/plugins folder contains all the Mica plugins that will be inspected at startup. A plugin is enabled if it has:

* A valid plugin.properties file,
* In case of several versions of the same plugin are installed, the latest one is selected.

The layout of the plugin folder is as follow:

.. code-block:: text

  MICA_HOME/
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

Mica assigns a data folder location to the plugin: **MICA_HOME/data/<plugin-name>** where plugin-name is the name defined in the plugin.properties file. This folder is then the one to be backed-up.
