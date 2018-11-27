group
=====

Groups values from a continuous space into a discrete space given a list of adjacent range limits. Applies only to integer or decimal type values. The returned value is:

* the text representation of the range, for instance:
  * '-10' for range (-∞‥10),
  * '10-20' for range [10..20),
  * '20+' for range [20..+∞).
* the text representation of the value if the value is defined as an outlier.

See also :doc:`../value/map`.

Syntax
------

.. code-block:: javascript

  group(array_of_bounds[, array_of_outliers])

===================== ============================
Parameter             Description
===================== ============================
``array_of_bounds``   A list of values that will be the bounds of the ranges.
``array_of_outliers`` An optional list of outlier values that will be not be grouped and will be returned as is.
===================== ============================

Examples
--------

Usage example, possible returned values are: ``-18``, ``18-35``, ``35-40``, ..., ``70+``

.. code-block:: javascript

  $('CURRENT_AGE').group([18,35,40,45,50,55,60,65,70]);

Support of optional outliers:

.. code-block:: javascript

  $('CURRENT_AGE').group([18,35,40,45,50,55,60,65,70],[888,999]);

In combination with map:

.. code-block:: javascript

  $('CURRENT_AGE').group([30,40,50,60],[888,999]).map({
     '-30' :  1,
     '30-40': 2,
     '40-50': 3,
     '50-60': 4,
     '60+':   5,
     '888':   88,
     '999':   99
   });
