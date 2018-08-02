newSequence
===========

Creates a new value sequence object. A value sequence is-a value object but also has-some value objects (see Value Sequence Methods).

See also :doc:`newValue`, :doc:`../sequence/asSequence`.

Syntax
------

.. code-block:: javascript

  newSequence(data[,type])

=============== ============================
Parameter       Description
=============== ============================
``data``        The data to be wrapped in the value object. If an array is provided, each item will be wrapped in a value object and added to the value sequence.
``type``        The value type to be used to interpret the data. If not provided the type is guessed (as much as possible) from the data. See Value Types section for a complete list of types and supported value formats.
=============== ============================

Examples
--------

Create some value sequences:

.. code-block:: javascript

  // Creates a value sequence of type 'text' with one item
  newSequence('lorem ipsum')

  // Creates a value sequence of type 'integer' with one item
  newSequence(123)

  // Creates a value sequence of type 'integer' with one item
  newSequence('123','integer')

  // Creates a value sequence of type 'text' with 3 items
  newSequence(['a','b', 'c'])
