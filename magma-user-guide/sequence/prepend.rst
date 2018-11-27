prepend
=======

Prepends (adds at the beginning) a value to a value to produce a value sequence. Also accepts a value sequence as input, in which case, both sequences are concatenated to produce a single one (it does not produce a sequence of sequence).

If the value being added is not of the same type as the sequence, it will be converted to the sequence's type. If the conversion fails, an exception is thrown.

If the sequence is null or empty, this method returns a new sequence containing the parameter(s). If the parameter is null, a null value is appended.

See also :doc:`append`, :doc:`insertAt`, :doc:`push`.

Syntax
------

.. code-block:: javascript

  prepend(value [,value])

=============== ============================
Parameter       Description
=============== ============================
``value``       The value(s) to prepend to the sequence
=============== ============================

Examples
--------

.. code-block:: javascript

  // Add a value to a sequence, then compute the average of the resulting sequence
  $('BloodPressure:Measure.RES_PULSE').prepend($('StandingHeight:FIRST_RES_PULSE')).avg();

  // Prepend several values to a value to produce the sequence: b, c, null, a
  newValue('a').prepend('b', 'c', null);

  // Prepend several values to a value sequence to produce the sequence: c, d, null, a, b
  newSequence(['a', 'b']).prepend('c', 'd', null);
