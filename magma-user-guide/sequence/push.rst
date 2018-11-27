push
====

Adds (at the end) a value to a value to produce a value sequence. Also accepts a value sequence as input, in which case, both sequences are concatenated to produce a single one (it does not produce a sequence of sequence).

If the value being added is not of the same type as the sequence, it will be converted to the sequence's type. If the conversion fails, an exception is thrown.

If the sequence is null, this method returns a null sequence (this part is different from :doc:`append`). If the sequence is empty, this method returns a new sequence containing the parameter(s). If the parameter is null, a null value is appended.

See also :doc:`append`, :doc:`insertAt`, :doc:`prepend`.

Syntax
------

.. code-block:: javascript

  push(value [,value])

=============== ============================
Parameter       Description
=============== ============================
``value``       The value(s) to append to the sequence
=============== ============================

Examples
--------

.. code-block:: javascript

  // Add a value to a sequence, then compute the average of the resulting sequence
  $('BloodPressure:Measure.RES_PULSE').push($('StandingHeight:FIRST_RES_PULSE')).avg();
