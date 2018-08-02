log
===

Provides *info* level logging of messages and variable values.

Syntax
------

.. code-block:: javascript

  log(text[, value_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``text``        The text to be logged. May contain place holders for values.
``value_i``     One of the value to be replaced in the text by order of appearance.
=============== ============================

Examples
--------

.. code-block:: javascript

  log('My message');
  log('Do you smoke ? {}', $('DO_YOU_SMOKE'));
