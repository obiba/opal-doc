firstNotNull
============

Returns the first Value object of the sequence which value is not null. If the value sequence is empty or if there aren't not null values in the sequence a Value object with a null value is returned.

See also :doc:`empty`, :doc:`first`, :doc:`last`, :doc:`valueAt`, :doc:`size`.

Syntax
------

.. code-block:: javascript

  firstNotNull()

Examples
--------

.. code-block:: javascript

  $('Admin.StageInstance.stage').firstNotNull()
