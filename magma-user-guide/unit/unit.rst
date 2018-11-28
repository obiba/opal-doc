unit
====

Sets or gets the measurement unit:

* when called without any arguments, this method returns the current measurement unit of the value.
* when called with a string argument, this method sets the measurement unit of the current value, regardless of the previous measurement unit (if any).

See also :doc:`toUnit`.

Syntax
------

.. code-block:: javascript

  unit([value])

=============== ============================
Parameter       Description
=============== ============================
``value``       The optional new measurement unit (must be a string).
=============== ============================

Examples
--------

.. code-block:: javascript

  $('HEIGHT').unit() // returns 'cm'
  $('HEIGHT').unit('m') // returns the same value, but with a measurement unit of 'm'
