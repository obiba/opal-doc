root
====

Returns the root of the value.

See also :doc:`cbroot`, :doc:`sqroot`.

Syntax
------

.. code-block:: javascript

  root(root)

=============== ============================
Parameter       Description
=============== ============================
``root``        The root to evaluate.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').root(2) // same as sqroot()
  $('AVar').root(3) // same as cbroot()
