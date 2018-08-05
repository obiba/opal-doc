attribute
=========

Get the variable attribute value with the given name.

See also :doc:`../global/variable`.

Syntax
------

.. code-block:: javascript

  attribute(name)

=============== ============================
Parameter       Description
=============== ============================
``name``        The name that identifies the attribute.
=============== ============================

Examples
--------

Get the value corresponding to the 'stage' attribute:

.. code-block:: javascript

  $var('AVG_SITTING_HEIGHT').attribute('stage')
