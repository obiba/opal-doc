matches
=======

Returns a Boolean value after match of a regular expression against a string. See `Regular Expressions in JavaScript Guide <https://developer.mozilla.org/en/Core_JavaScript_1.5_Guide/Regular_Expressions#Writing_a_Regular_Expression_Pattern>`_ for more details about how to write a regular expression pattern.

See also :doc:`replace`.

Syntax
------

.. code-block:: javascript

  matches(regex)

=============== ============================
Parameter       Description
=============== ============================
``regex``       The regular expression to be searched for.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('VarName').matches(/yes/)
