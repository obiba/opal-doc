length
======

Returns the length of the value. The length of a value has different meanings depending on the value type:

* if value type is binary the length is the number of bytes of the value,
* else the length is number of characters of the string representation of the value.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  length()

Examples
--------

Get the binary value's length in bytes:

.. code-block:: javascript

  $('BINARY').length()
