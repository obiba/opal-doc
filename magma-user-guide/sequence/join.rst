join
====

Joins the text representation of the values in the sequence, using the provided delimiter, prefix and suffix. A null (resp. empty sequence) will return a null (resp. empty) text value.

See also :doc:`zip`.

Syntax
------

.. code-block:: javascript

  join([delimiter[, prefix[, suffix]]])

=============== ============================
Parameter       Description
=============== ============================
``delimiter``   The delimiter text (string or value) to be used to join values of the sequence.
``prefix``      The prefix text (string or value) to be added at the beginning of the resulting text (will not be applied if empty).
``suffix``      The suffix text (string or value) to be added at the end of the resulting text (will not be applied if empty).
=============== ============================

Examples
--------

Join the value sequence: [1,2,3]

.. code-block:: javascript

  // returns "1, 2, 3"
  $('SequenceVar').join(', ');
  // returns "[1:2:3]"
  $('SequenceVar').join(':', '[', ']');
  // returns "123"
  $('SequenceVar').join();
