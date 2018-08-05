type
====

Returns or changes the value's type. This conversion can be destructive (lose precision) or impossible (convert 'ABC' to an integer). When the conversion is impossible, the script's evaluation fails.

Improvement to consider: when conversion fails return null instead of throwing an exception.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  type([name])

=============== ============================
Parameter       Description
=============== ============================
``type``        | Optional type name into which the value shall be converted. Possible values are (case insensitive):
                | ``text``, ``integer``, ``decimal``, ``boolean``, ``locale``, ``datetime``, ``date``, ``binary``, ``point``, ``linestring``, ``polygon`` (see :ref:`value-types` description).
=============== ============================

Examples
--------


.. code-block:: javascript
