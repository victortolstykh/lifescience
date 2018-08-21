You can search over your database for reaction
`SMARTS <http://www.daylight.com/dayhtml/doc/theory/theory.smarts.html>`__
expression match with the following query:

::

    SELECT * FROM $table WHERE Bingo.RSMARTS($column, $rsmarts)=1;
