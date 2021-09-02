.. _magmajs:

Magma JS Introduction
=====================

The Magma Javascript API is there to allow accession of data and data dictionary in order to perform data cleansing, data harmonization, data filtering etc.

Syntax
------

Selectors and Execution context
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The API offers a simple way to access to variables and variable value for a value set, based on Magma naming schema. A javascript is always defined within a context that defines implicitly the object to which the selection is applied.

See selectors description: $ and $var.

Chaining
~~~~~~~~

Methods from this API return an object to which a method can be directly applied. This allow method calls chaining, for instance:

.. code-block:: javascript

  $('DO_YOU_SMOKE').any('DNK', 'PNA').not()

Using Selection Statements
--------------------------

To use JavaScript selection statements such as if-else and switch first convert Magma ScriptableValues to native JavaScript values using the .value() method. Here are some examples:

if-else
~~~~~~~

.. code-block:: javascript

  if($('BooleanType.blood.contraindicated').value()) {
     log('Blood collection has been contraindicated');
  }
  if($('IntegerType.tubes.collected').gt($('IntegerType.tubes.expected')).value()) {
     log('More tubes than expected.');
  } else if ($('IntegerType.tubes.collected').lt($('IntegerType.tubes.expected')).value()) {
     log('Less tubes than expected.');
  } else {
     log('Collected tubes matches expected tubes.');
  }

switch
~~~~~~

.. code-block:: javascript

  switch($('Admin.Participant.gender').value()) {
     case "MALE":
        log('Participant is male.');
     case "FEMALE":
        log('Participant is female.');
     default:
        log('Participant gender is unknown.');
  }

Advanced Configuration
----------------------

The javascript engine allows several levels of optimization, usually a compromise between compilation time and execution time.

The optimization level can be specified as a JVM system property, i.e. with the command line argument ``-Drhino.opt.level=<level>`` where level is a number between -1 (js code is interpreted) and 9 (js code is compiled and optimized as much as possible). See more about `Rhino Optimization <https://developer.mozilla.org/en-US/docs/Mozilla/Projects/Rhino/Optimization>`_. In some rare cases the compilation can fail because the script is (very) large: in this situation the optimization level should be set to -1.
