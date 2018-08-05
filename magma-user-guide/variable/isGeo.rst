isGeo
=====

Returns whether the variable value type is ``point``, ``linestring`` or ``polygon``, as a Boolean value.

See also :doc:`../global/variable`.

Syntax
------

.. code-block:: javascript

  isGeo()

Examples
--------

.. code-block:: javascript

  $var('PostalCode.area').isGeo()
