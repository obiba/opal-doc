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

.. _resource_view:

Add View
~~~~~~~~

A view can be created over a resource. This operation is relevant only if the resource can be coerced to a tabular representation. Having a view over a resource allows to give a visibility to the data dictionary and the summary statistics of the resource, for the purpose of data documentation (in `Mica <https://micadoc.obiba.org>`_ for instance).

This view will establish a connection with a resource object in a background R server session. If the resource connection requires a specific R package that is installed only in a specific R server, Opal will try to guess the most appropriate R server profile or the R server profile name can be provided. The variables of the view will be initialized with the observed columns of the tibble's representation of the resource. The identifiers will be extracted from the first column, or from the one specified in the view creation form. The values will be queried from the underlying tibble object.

After the resource's view has been created, it is possible to rename variables, change their value type, manage categories and annotate them with taxonomy terms. It is not possible to make more complex derived variables, such as advanced data transformation or the combination with other column values.

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
