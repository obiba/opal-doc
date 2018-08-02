source
======

This method allows to load a javascript library by specifying a path to a file. The result of this method is like in-lining javascript code in the current script. The loaded javascript libraries can be used for defining frequently used functions and easily reuse them across multiple scripts.

Syntax
------

.. code-block:: javascript

  source(path)

=============== ============================
Parameter       Description
=============== ============================
``path``        The path to the javascript file. The path must be absolute in the Opal file system.
=============== ============================

Examples
--------

Define a javascript file with the following code located in Opal file system at path **/project/questionnaires/lib/age.js**:

.. code-block:: javascript

  /*
   * Calculate the age from 2 arguments:
   *   birthDate: date of birth value
   *   otherDate: date to compare with
   */
  function age(birthDate, otherDate) {
      var years = otherDate.year().minus(birthDate.year());

      if (otherDate.month().lt(birthDate.month()).value() ||
          otherDate.month().eq(birthDate.month()).value() && otherDate.dayOfMonth().lt(birthDate.dayOfMonth()).value()) {
          years = years.minus(1);
      }

      return years;
  }


Then load this javascript file by specifying its location:

.. code-block:: javascript

  // load the library that defines the age() function
  source('/project/questionnaires/lib/age.js');

  // then use the age() function:
  //   age at the time of the interview
  age($('DATE_OF_BIRTH'), $('INTERVIEW_DATE'));
  //   or age at the time of the script execution
  age($('DATE_OF_BIRTH'), now());
