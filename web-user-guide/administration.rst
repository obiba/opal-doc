Administration
==============

Opal manages databases for two distinct purposes: for holding the participants identifiers and for holding the variable catalog and participant data. Since Opal 3.0, it is not required to set up neither an identifiers database, nor a data database:

* If no identifiers database is defined, the :ref:`ids` service when performing import/export will be disabled.
* If no data database is defined, no data can be imported in any project, only :ref:`resources` can be defined and used for analysis.


.. toctree::
   :maxdepth: 1
   :caption: System

   administration/general-settings
   administration/identity-providers
   administration/r
   administration/datashield
   administration/taxonomies
   administration/databases
   administration/plugins
   administration/apps
   administration/jvm
