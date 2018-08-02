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

Methods
-------

Global Methods
~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`global/value`     Return the variable value within the current value set.
:doc:`global/this`      Return the variable value within the current view value set.
:doc:`global/join`      Return the joined variable value referenced by a variable value within the current value set.
:doc:`global/group`     Return a map of variable values in the same group of occurrence within the current value set.
:doc:`global/id`        Return the entity identifier within the current value set.
:doc:`global/variable`  Returns the variable object at the given name.
======================= ===========================================================

Variable Methods
~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Value Methods
~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Value Sequence Methods
~~~~~~~~~~~~~~~~~~~~~~

============================ ===========================================================
Methods                      Description
============================ ===========================================================
:doc:`sequence/firstNotNull` Returns the first not null value in a value sequence.
============================ ===========================================================

Boolean Value Methods
~~~~~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Numeric Value Methods
~~~~~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Measurement Unit Methods
~~~~~~~~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Text Value Methods
~~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Date and Datetime Value Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

Geo Value Methods
~~~~~~~~~~~~~~~~~

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

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
