asSequence
==========

Turns a value object into a value sequence object. A value sequence *is-a* value object but also *has-some* value objects. If the value object on which it is applied is already a value sequence object, no operation is made.

See also :doc:`../global/newValue`, :doc:`../global/newSequence`, :doc:`isSequence`.

Syntax

.. code-block:: javascript

  asSequence()

Examples

Create some value sequences:

.. code-block:: javascript

  // Creates a value sequence of type 'text' with one item
  newValue('lorem ipsum').asSequence()

  // Make sure that the value returned by $group is always a value sequence
  $group('Var1','key','Var2').asSequence()
