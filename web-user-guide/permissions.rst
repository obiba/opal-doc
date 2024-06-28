Permissions
===========

Permissions are defined per entity to be accessed: a table, a resource, a project, the DataSHIELD service etc. Note that the following rules apply:

* By default, no permissions is granted (apart of user's home folder).
* When an entity is part of a hierarchy (a variable is in a table which is in a project), the parent entities are de-facto read-only.
* When an entity is created, the creator has full access to it, including the permission to delete or grant access permission to it.
* When an entity refers to another entity, the most restrictive permissions applies.

Project
-------

Depending on the permission applied to the considered entity, the services DataSHIELD, R, SQL and Export/Copy may be or not available (driven by the ability to see the individual values).

Note that the R and the DataSHIELD services require an additional specific usage permission.


.. list-table::
  :header-rows: 1

  * - Resource
    - Permission
    - Description
  
  * - A project
    - **Administrate** project
    - Full access to the project.

Tables
~~~~~~

.. list-table::
  :header-rows: 1

  * - Entity
    - Permission
    - Description
    - DataSHIELD
    - R
    - SQL
    - Export/Copy

  * - A project
    - **Add tables**
    - | Tables (or views) can be created, either directly or using the import data process.
      | Full access to the created tables is automatically granted.
    - x
    - x
    - x
    - x

  * - A table
    - | **View** table dictionary
      | **View** summaries
    - Read only access to the table dictionary and data summaries (no access to individual values).
    - x
    -
    - 
    -

  * - A table
    - | **View** table dictionary
      | **View** values
    - Read only access to the table dictionary and individual data.
    - x
    - x
    - x
    - x
  
  * - A table
    - | **Edit** table dictionary
      | **View** summaries
    - Edit dictionary and view values summary (no access to individual values).
    - x
    - 
    - 
    - 

  * - A table
    - | **Edit** table dictionary
      | **View** values
    - Edit dictionary and view individual values.
    - x
    - x
    - x
    - x

  * - A table
    - **Administrate** table
    - Full access to the table, including edition of the dictionary and individual values.
    - x
    - x
    - x
    - x

  * - A variable
    - | **View** variable
      | **View** summary
    - Read only access to the variable description and its values summary (no access to individual values).
    - x
    - x
    - x
    - x
  
Resources
~~~~~~~~~

Strictly speaking, permissions are granted to resource references, i.e. it is the ability to connect to a resource that is considered. The resource itself is not directly accessible.

.. list-table::
  :header-rows: 1

  * - Entity
    - Permission
    - Description
    - DataSHIELD
    - R
  
  * - A project
    - **View** any resource
    - View any resource without having access to the associated credentials.
    - x
    - 

  * - A project
    - **Administrate** resources
    - Full access to the project resources.
    - x
    - x

  * - A resource
    - **View** resource
    - View resource without having access to the associated credentials.
    - x
    - 

  * - A resource
    - **Adinistrate** resource
    - Full access to the resource.
    - x
    - x

System
------

.. list-table::
  :header-rows: 1

  * - Entity
    - Permission
    - Description

  * - System
    - **Add** project
    - Add new projects and therefore can import/export data in the context of the project.
  
  * - System
    - **Administrate**
    - Full access to the system: configuration, users and groups, permissions, taxonomies, databases, R servers, DataSHIELD profiles etc. This is the highest levl of permissions.
  
  * - R service
    - **Use**
    - Use the R service.

  * - DataSHIELD service
    - **Use**
    - Use the DataSHIELD service.

  * - DataSHIELD service
    - **Administrate**
    - Administrate the DataSHIELD service: manage R packages, add and modify profiles.

  * - DataSHIELD service
    - **Use profile**
    - When a DataSHIELD profile access is restricted, the use of the profile also grants the use permission of the DataSHIELD service.
