The ``Bingo.CANSMILES()`` operator can be used for generating canonical
SMILES of Molfiles, other SMILES, or binary molecules. The operator
works equally well with CLOB, BLOB, and VARCHAR2 operands. The operator
always returns the VARCHAR2 result.

::

    SELECT Bingo.CanSMILES($molfile) FROM DUAL;

    SELECT Bingo.CanSMILES($column) FROM $table;

Bingo Canonical SMILES is, according to Daylight and ChemAxon
terminology, unique SMILES with isomeric information, or *absolute*
SMILES. All significant molecular features, such as isotopes, charges,
radicals, stereocenters, stereogroups, cis-trans bonds, and aromaticity,
are encoded into SMILES in a canonical form. A canonical SMILES string
defines the molecule independently of any particular representation
(atoms renumbering, stereogroups renumbering, explicit/implicit
hydrogens). So, the equality of canonical SMILES of two molecules
guarantees that these molecules are the same, and vice versa:

::

    Bingo.CANSMILES($a) = Bingo.CANSMILES($b)

*if and only if*

::

    Bingo.Exact($a, $b, 'ALL') = 1

**Note:** A canonical SMILES computation can only be done for database
molecules. Query features are not supported.

**Note:** If the input molecule is badly formed (i.e. does not conform
to any format, has drawing mistakes or has unsupported features), Bingo
throws an exception to Oracle.
