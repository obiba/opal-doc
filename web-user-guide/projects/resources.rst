.. _resources:

Project Resources
=================

Some reference to :ref:`intro-resources` can be defined within a project. The resource types are discovered by scanning the R packages in the R server (restarting the R server triggers a new package scan) and find the ones implementing the `Resource Forms <https://github.com/obiba/resourcer#resource-forms>`_ API. Then extending Opal to new type of resources is just a matter of installing the appropriate R package (see :ref:`r-packages` documentation).

See also documentation of resource reference details:

.. toctree::
   :maxdepth: 1

   resource-details

Permissions
-----------

Specify the access rights to any resource of the project.

View any resource Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

View any resource without having access to the associated credentials (DataSHIELD compliant permission).

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Allow all operations on any resource of the project (including addition and removal).

Operations
----------

Add Resource
~~~~~~~~~~~~

To perform a resource addition the user is proposed to select the resource category and then select the appropriate resource type. Note that the same resource type can belong to several categories: these categories usually represents the data format, the way to access the resource or the domain of interest etc. The associated resource form will capture the different elements of the resource reference details (parameters and credentials), from which the R resource object will be built on R user request.

Edit Resource
~~~~~~~~~~~~~

The edition of a single resource can be done from the list of resource references. A resource reference cannot be renamed, instead use the :ref:`duplicate-operation` operation to declare the same resource with a different name.

Remove Resource
~~~~~~~~~~~~~~~

Single or bulk removal of resource references (the underlying data management system is not affected).
