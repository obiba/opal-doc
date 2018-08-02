$id, $identifier
================

The current object is a value set. $id will access to the entity Opal identifier within this value set.

See also :doc:`value`, :doc:`join`, :doc:`variable`.

Syntax
------

.. code-block:: javascript

  $id()
  // alternate syntax
  $identifier()

Examples
--------

Correct a particular value of an entity given its identifier. Other entities will return the recorded value for variable DO_YOU_SMOKE.

.. code-block:: javascript

  $id().map({'778834' : 'NO'}, $('DO_YOU_SMOKE'))
