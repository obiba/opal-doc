Magma JS Introduction
=====================

The Magma Javascript API is there to allow accession of data and data dictionary in order to perform data cleansing, data harmonization, data filtering etc.

Syntax
------

Selectors and Execution context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The API offers a simple way to access to variables and variable value for a value set, based on Magma naming schema. A javascript is always defined within a context that defines implicitly the object to which the selection is applied.

See selectors description: $ and $var.

Chaining
~~~~~~~~

Methods from this API return an object to which a method can be directly applied. This allow method calls chaining, for instance:

.. code-block:: javascript

  $('DO_YOU_SMOKE').any('DNK', 'PNA').not()
