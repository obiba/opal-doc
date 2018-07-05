Plugins
=======

Plugins can be managed from the administration page:

* installed plugins
* plugins that can be upgraded
* new plugins that can be installed
* plugin manual installation
* plugins repository reference

Installed
---------

The installed plugins are listed. Some operations can be performed on each plugin:

* a plugin is executed as a service which can be restarted.
* a plugin can be configured by editing the plugin's site.properties file. Depending on the plugin installation it can be necessary to restart the plugin so that the new configuration become effective.
* a plugin can be removed: it is in fact marked as being ready for removal and is still operational until the next Opal restart.

Updates
-------

The plugin repository is inspected to list if some installed plugins have a most recent version available for install (according to the current Opal version).

Available
---------

The plugin repository is inspected to list the plugins that are not installed and are available for installation (according to the current Opal version).

Advanced
--------

Plugin Archive Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is possible to install manually a plugin from its archive distribution. User is responsible for ensuring that the plugin applies to the current Opal version. The installation is effective at Opal restart.

Update Site
~~~~~~~~~~~

A plugin repository can be configured so that Opal can query the plugin updates and availability for installation. See ``org.obiba.opal.plugins.site`` property in :ref:`misc-config` instructions.
