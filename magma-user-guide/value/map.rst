map
===

Uses a lookup table to map the a value to another (which may be computed or derived). When the value to be mapped is not found in the association table, then:

* if a value is specified for null values, this value is returned,
* else if a default value is specified, the default value is returned,
* else null is returned.

Another way to use this method is to provide a mapping javascript function, especially useful for value sequences.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  map({key_1:value_1[, key_i:value_i[, ...]]}[, defaultValue[, nullValue]])
  map(mapper)

.. list-table::
   :header-rows: 1
   :widths: 10 90

   * - Parameter
     - Description
   * - ``key_i:value_i``
     - A list of key/value pairs: the value to be mapped and the mapping value, explicitly provided or the result of an operation or a function.
   * - ``defaultValue``
     - optional value to return when the lookup value is not found in the list of key/value pairs. (since Opal 1.5.1 and Onyx 1.8.3)
   * - ``nullValue``
     - optional value to return when the lookup value is null.
   * - ``mapper``
     - a mapping javascript function called for each value (with arguments: value and index of the value in the sequence) and that returns the resulting mapped value.

Examples
--------

Simple constant lookup table

============== =============
Value          Mapping Value
============== =============
'NO'           0
'YES'          1
'DNK'          8888
anything else  9999
============== =============

.. code-block:: javascript

  $('SMOKE').map(
    {'NO':0,
     'YES':1,
     'DNK':8888}, 9999)

Lookup table with computed mapped values

======== ==============
Value    Mapped Value
======== ==============
'AGE'    the value of the 'SMOKE_ONSET_AGE' variable
'YEAR'   compute the value 'SMOKE_ONSET_YEAR' minus the year part of the 'BIRTH_DATE' variable
'DNK'    8888
'PNA'    9999
null     7777
======== ==============

.. code-block:: javascript

  $('SMOKE_ONSET').map(
    {'AGE':$('SMOKE_ONSET_AGE'),
     'YEAR':$('SMOKE_ONSET_YEAR').minus($('BIRTH_DATE').year()),
     'DNK':8888,
     'PNA':9999}, null, 7777)

Note that all the mapped values will be computed, regardless of the input. If the computation is expensive, consider using a function to compute it, as it will only be invoked when required. See below for an example.

Accepts sequences and returns sequences. In the following example, if the input is 'FRENCH,ENGLISH', the output will be '0,1'.

.. code-block:: javascript

  $('LANGUAGES_SPOKEN').map({'FRENCH':0, 'ENGLISH':1});

The value can also be computed by executing an arbitrary function. This can be used to lazily evaluate mapped values.

.. code-block:: javascript

  // Can execute function to calculate lookup value
  $('BMI_DIAG').map(
    {'OVERW': function(value) {
                // 'OVERW' is passed in as the method's parameter
                // some expensive computation happens only when the input actually is 'OVERW'
                return expensiveValue;
              },
     'NORMW': 0
    });

Functions can also be passed to define the default value and/or the null value.

.. code-block:: javascript

  $('LANGUAGES_SPOKEN').map({'FRENCH': 'FR', 'ENGLISH': 'EN'}, function(val) { return val.substring(0, 2) }, function() { return '??' })

A mapping function can pe provided in place of the mapping object and the additional values (null and default).

.. code-block:: javascript

  $('LANGUAGES_SPOKEN').map(function(val,idx) { return val.isNull().value() ? '??' : val.value().substring(0,2) })
