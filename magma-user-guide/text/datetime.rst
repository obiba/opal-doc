datetime
========

Makes a value of datetime type by parsing the text value given a date format pattern.

The pattern should be defined from the `Java Date Format Specifications <http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html>`_:

======= ================================================= =====================================
Letter  Date or time component                            Example
======= ================================================= =====================================
G       Era designator                                    AD
y       Year                                              1996; 96
Y       Week year                                         2009; 09
M       Month in year                                     July; Jul; 07
w       Week in year                                      27
W       Week in month                                     2
D       Day in year                                       189
d       Day in month                                      10
F       Day of week in month                              2
E       Day name in week                                  Tuesday; Tue
u       Day number of week (1 = Monday, ..., 7 = Sunday)  1
a       Am/pm marker                                      PM
H       Hour in day (0-23)                                0
k       Hour in day (1-24)                                24
K       Hour in am/pm (0-11)                              0
h       Hour in am/pm (1-12)                              12
m       Minute in hour                                    30
s       Second in minute                                  55
S       Millisecond                                       978
z       Time zone                                         Pacific Standard Time; PST; GMT-08:00
Z       Time zone                                         -0800
X       Time zone                                         -08; -0800; -08:00
======= ================================================= =====================================

See also :doc:`date`.

Syntax
------

.. code-block:: javascript

  datetime(format)

=============== ============================
Parameter       Description
=============== ============================
``format``      The date format pattern to be used.
=============== ============================

Examples
--------

.. code-block:: javascript

  // example: 08/23/73
  $('AVar').datetime('MM/dd/yy')

  // example: 10/23/12 10:59 PM
  $('AVar').datetime('MM/dd/yy h:mm a')

  // example: Wed, 4 Jul 2001 12:08:56 -0700
  $('AVar').datetime('EEE, d MMM yyyy HH:mm:ss Z')

  // example: 2008-03-01T13:00:00+01:00
  $('AVar').datetime("yyyy-MM-dd'T'HH:mm:ssZ")
