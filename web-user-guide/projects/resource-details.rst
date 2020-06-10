.. _resource:

Resource
========

Details of a reference to a resource can be displayed. Users not having the permission to see the credentials part of a resource will still be able to see its location. The resource page also displays information about the R package providing the resource type.

Permissions
-----------

Specify the access rights to a single resource.

View resource Permission
~~~~~~~~~~~~~~~~~~~~~~~~

View resource without having access to the associated credentials (DataSHIELD compliant permission).

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Allow all operations on the resource (including removal).

Operations
----------

Test Resource
~~~~~~~~~~~~~

Testing a resource will consist of assigning the resource reference into a R server session and verify that the resource type is correctly identified, i.e. the assigned R object is of class *ResourceClient* as defined by the `resourcer <https://github.com/obiba/resourcer>`_ R package. Note that this does not prove that the underlying data are accessible as getting these could be a deferred R operation.

Edit Resource
~~~~~~~~~~~~~

Edit the current resource, anything can be changed except the name.

.. _duplicate-operation:

Duplicate Resource
~~~~~~~~~~~~~~~~~~

Duplicate a resource (type, parameters and credentials), useful when several resources are defined in the same data management system (several SQL tables in the same database for instance). Also useful for changing the resource name.

Remove Resource
~~~~~~~~~~~~~~~

Remove a resource reference (the underlying data management system is not affected).
