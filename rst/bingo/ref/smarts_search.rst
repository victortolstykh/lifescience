You can search over your database for
`SMARTS <http://www.daylight.com/dayhtml/doc/theory/theory.smarts.html>`__
expression match with the following query:

::

    SELECT * FROM $table WHERE Bingo.SMARTS($column, $smarts)=1;

Differences between substructure and SMARTS matching
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

While a lot of SMARTS notation is allowed in ``Sub()`` operator queries
as well, there are differences between substructure and SMARTS search:

-  SMARTS fragments $(...) are not allowed in ordinary substructure
   search

-  Empty bond designator (like 'CC' or 'cc') denotes 'single or
   aromatic' bond in ``SMARTS()``. In ``Sub()``, it denotes aromatic
   bond, if it belongs to a ring and has both end atoms aromatic
   (lowercase); otherwise, it denotes a single bond.

-  'C' within ``SMARTS()`` means aliphatic carbon, while 'C' within
   ``Sub()`` means any carbon. The same applies to 'B', 'N', 'O', 'S',
   'P'. 'C1~C~C~C~C~C~1' won't match 'c1ccccc1' in ``SMARTS()``, but it
   will do so in ``Sub()``.

-  SMARTS queries are not fed to aromaticity matcher. 'c1-c=c-c=c-c=1'
   won't match 'c1ccccc1' in ``SMARTS()``, but it will do so in
   ``Sub()``.

-  Tautomer (``TAU``) and resonance (``RES``) matching options are not
   allowed within ``SMARTS()`` operator.
