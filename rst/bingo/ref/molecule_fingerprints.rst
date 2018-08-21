The ``Bingo.Fingerprint`` operator can be used to generate Indigo
fingerprints for molecule structures. The operator has two arguments:
molecule and options, and returns BLOB result.

::

    SELECT Bingo.Fingerprint($molecule, $type) FROM DUAL;

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
-  ``sub-res`` — "Resonance substructure fingerprint", useful for
   resonance substructure screening
-  ``sub-tau`` — "Tautomer substructure fingerprint", useful for
   tautomer substructure screening
-  ``full`` — "Full fingerprint", which has all the mentioned
   fingerprint types included
