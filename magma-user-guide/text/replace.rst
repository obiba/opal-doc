replace
=======

Used to find a match between a regular expression and a string, and to replace the matched substring with a new substring.

See also :doc:`matches`.

Syntax
------

.. code-block:: javascript

  replace(regex, text)

=============== ============================
Parameter       Description
=============== ============================
``regex``       The regular expression to be searched for.
``text``        The string that replaces the matched substring.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('VarName').replace(/yes/, '1')
