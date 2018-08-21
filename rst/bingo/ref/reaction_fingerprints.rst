The ``Bingo.RFingeprint`` operator can be used to generate Indigo
fingerprints for reaction structures. The operator has two arguments:
reaction and options and returns BLOB result.

::

    SELECT Bingo.Fingerprint($reaction, $type) FROM DUAL;

    SELECT Bingo.Fingerprint($binary, $type) FROM DUAL;

    SELECT Bingo.Fingerprint($column, $type) FROM $table;

The options are the same as for ``IndigoObject.fingerprint`` method from
the Indigo SDK described
`here <../indigo/api/index.html#fingerprints>`__.

The following fingerprint types are available:

-  ``sim`` — "Similarity fingerprint", useful for calculating similarity
   measures (the default)
-  ``sub`` — "Substructure fingerprint", useful for substructure
   screening
-  ``full`` — "Full fingerprint", which has all the mentioned
   fingerprint types included
