concat
======

Returns the text type result of first operand concat second operand. The operands must be either values or text type.

See also :doc:`capitalize`, :doc:`lowerCase`, :doc:`replace`, :doc:`trim`, :doc:`upperCase`.

Syntax
------

.. code-block:: javascript

  concat(value_1[, value_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``value_i``     The value which string representation is to be concatenated to the text value.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').concat($('OtherVar'));
