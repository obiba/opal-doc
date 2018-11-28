format
======
Returns the text representation of the date formatted by the provided pattern.

Date and time formats are specified by date and time pattern strings. The pattern should be defined from the `Java Date Format Specifications <http://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html>`_:

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

Pattern letters are usually repeated, as their number determines the exact presentation:

* Text: if the number of pattern letters is 4 or more, the full form is used; otherwise a short or abbreviated form is used if available.
* Number: the number of pattern letters is the minimum number of digits, and shorter numbers are zero-padded to this amount.
* Year: if the number of pattern letters is 2, the year is truncated to 2 digits; otherwise it is interpreted as a number.
* Month: if the number of pattern letters is 3 or more, the month is interpreted as text; otherwise, it is interpreted as a number.

The following examples show how date and time patterns are interpreted in the U.S. locale. The given date and time are 2001-07-04 12:08:56 local time in the U.S. Pacific Time time zone.

================================= ==============================
Date and Time Pattern             Result
================================= ==============================
``yyyy.MM.dd G, HH:mm:ss z``      2001.07.04 AD, 12:08:56 PDT
``EEE, MMM d, yy``                Wed, Jul 4, 01
``h:mm a``                        12:08 PM
``K:mm a, z``                     0:08 PM, PDT
``yyyyy.MMMMM.dd GGG hh:mm aaa``  02001.July.04 AD 12:08 PM
``EEE, d MMM yyyy HH:mm:ss Z``    Wed, 4 Jul 2001 12:08:56 -0700
``yyMMddHHmmssZ``                 010704120856-0700
``yyyy-MM-dd'T'HH:mm:ss.SSSZ``    2001-07-04T12:08:56.235-0700
================================= ==============================

Syntax
------

.. code-block:: javascript

  format(pattern)

=============== ============================
Parameter       Description
=============== ============================
``pattern``     The pattern describing the date and time format.
=============== ============================

Examples
--------

String pattern:

.. code-block:: javascript

  $('Date').format('dd/MM/yyyy')

Pattern extracted from the string representation of a variable value:

.. code-block:: javascript

  $('Date').format($('Pattern'))
