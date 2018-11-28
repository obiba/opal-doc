insertAt
========

Insert at a given position a value to a value to produce a value sequence. Also accepts a value sequence as input, in which case, both sequences are concatenated to produce a single one (it does not produce a sequence of sequence).

If the value being added is not of the same type as the sequence, it will be converted to the sequence's type. If the conversion fails, an exception is thrown.

If the sequence is null or empty, this method returns a new sequence containing the parameter(s) (this part is different from :doc:`push`). If the parameter is null, a null value is appended.

See also :doc:`append`, :doc:`prepend`, :doc:`push`.

Syntax
------

.. code-block:: javascript

  insertAt(position, value [,value])

=============== ============================
Parameter       Description
=============== ============================
``position``    The position (0-based) at which the value is to be inserted. If this position is greater than the original value sequence length, null values will be inserted as well until the requested position.
``value``       The value(s) to insert in the sequence
=============== ============================

Examples
--------

.. code-block:: javascript

  // Add a value to a sequence, then compute the average of the resulting sequence
  $('BloodPressure:Measure.RES_PULSE').instertAt(0, $('StandingHeight:FIRST_RES_PULSE')).avg();

  // Insert several values to a value to produce the sequence: a, b, c, null
  newValue('a').insertAt(1, 'b', 'c', null);

  // Insert several values to a value to produce the sequence: a, null, b, c, null
  newValue('a').insertAt(2, 'b', 'c', null);

  // Insert several values to a value sequence to produce the sequence: a, c, d, null, b
  newSequence(['a', 'b']).insertAt(1, 'c', 'd', null);
