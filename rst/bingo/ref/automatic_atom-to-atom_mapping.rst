Description and Syntax
^^^^^^^^^^^^^^^^^^^^^^

The following Bingo operator is used to compute reaction AAM:

::

    Bingo.AAM($reaction, $strategy)

You can get the resulting reaction by selecting it from the ``DUAL``
table:

::

    SELECT Bingo.AAM($reaction, $strategy) FROM DUAL;

As ``$reaction`` you can specify VARCHAR2, CLOB, or BLOB containing
reaction SMILES, Rxnfile of binary reaction.

``$strategy`` is one of the following VARCHAR2 strings:

-  ``DISCARD``: discards the existing mappings entirely and considers
   only the existing reaction centers.
-  ``KEEP``: keeps the existing mapping and maps unmapped atoms.
-  ``ALTER``: alters the existing mapping, and maps the rest of the
   reaction but may change the existing mapping.
-  ``CLEAR``: removes the mappings from the reaction.

**Note:** In the 'KEEP' and 'ALTER' modes, any possible contradictions
between the existing mapping and the reaction centers are resolved by
correcting the reacting centers.

As a result, the operator always returns CLOB with Rxnfile.

**Note:** In case the given reaction does not have atom positions (i.e.
is represented as a reaction SMILES or binary format without atom
positions), the automatic reaction layout is performed.

Examples
^^^^^^^^

Building the mapping from reacting centers (``DISCARD`` mode):

Source Reaction

|image399|

Resulting Reaction

|image400|

Keeping the existing mapping (``KEEP`` mode). Note also the change in
the 3-7 reacting center:

Source Reaction

|image401|

Resulting Reaction

|image402|

Altering the existing mapping (``ALTER`` mode). Note the correction of
bond 16-18, the renumbering of mapped atoms and numbering of the
unmapped atoms:

Source Reaction

|image403|

Resulting Reaction

|image404|

Clearing the mapping (``CLEAR`` mode):

Source Reaction

|image405|

Resulting Reaction

|image406|
