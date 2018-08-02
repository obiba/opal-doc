newValue
========

Creates a new value object.

See also :doc:`../sequence/asSequence`, :doc:`newSequence`.

Syntax
------

.. code-block:: javascript

  newValue(data[,type])

=============== ============================
Parameter       Description
=============== ============================
``data``        The data to be wrapped in the value object.
``type``        The value type to be used to interpret the data. If not provided the type is guessed (as much as possible) from the data. See :ref:`value-types` section for a complete list of types and supported value formats.
=============== ============================

Examples
--------

Create some values:

.. code-block:: javascript

  // Creates a value of type 'text'
  newValue('lorem ipsum')

  // Creates a value of type 'integer'
  newValue(123)

  // Creates a value of type 'integer'
  newValue('123','integer')
  The created value object can be turned into a value sequence:

  // Creates a value sequence: 123, 234
  newValue(123).push(234)

  // Creates a value sequence of one item
  newValue(123).asSequence()
  When creating a date/datetime value, the type must be explicit and the data must be textual. See Value Types section for the date/datetime supported formats.

  // Creates a date value by parsing the provided text using "yyyy-MM-dd" format
  newValue('2013-03-24', 'date')

  // Creates a datetime value by parsing the provided text using "yyyy-MM-dd HH:mm" format
  newValue('2013-03-24 10:56', 'datetime')

  // Currently not supported
  newValue(new Date())
