Bingo supports the following molecule formats:

-  Daylight SMILES with ChemAxon extensions
-  Daylight SMARTS
-  MDL (Symyx) Molfile
-  GZip-compressed Molfile
-  CML
-  Internal binary format

Bingo supports the following reaction formats:

-  Daylight reaction SMILES with ChemAxon Extensions
-  Daylight reaction SMARTS
-  MDL (Symyx) Rxnfile
-  GZip-compressed Rxnfile
-  CML
-  Internal binary format

Daylight Formats with ChemAxon Extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Almost all features of the original Daylight
`SMILES <http://www.daylight.com/dayhtml/doc/theory/theory.smiles.html>`__
format are supported, including:

-  Aromatic rings
-  Hydrogen counters
-  Tetrahedral and allene-like stereocenters
-  Cis-trans double bonds
-  Disconnected structures
-  Reaction atom-to-atom mapping (AAM)

The only features that are not supported are:

-  Square-planar, trigonal-bipyramidal, octahedral stereo configurations

Almost all features of the original Daylight
`SMARTS <http://www.daylight.com/dayhtml/doc/theory/theory.smarts.html>`__
format are supported, including:

-  Aromatic and aliphatic atoms
-  SSSR (smallest set of smallest rings) calculation
-  Logical operators
-  Atom environments (nested SMARTS)
-  Component-level grouping

The only features that are not supported are:

-  Constraint "h" (implicit hydrogen count). Hydrogens can be stored
   implicitly or explicitly in the database, and we believe that this
   difference should not affect the search results. "H" (total hydrogen
   count) may be used instead
-  All features of SMILES format that are not supported

The following ChemAxon SMILES
`extensions <http://www.chemaxon.com/marvin/help/formats/cxsmiles-doc.html>`__
are supported:

-  Radical numbers: monovalent, divalent singlet, and divalent triplet
-  `Stereogroups <http://www.chemaxon.com/jchem/doc/user/query_stereochemistry.html>`__
-  Pseudo-atoms (atom aliases)
-  Fragment level grouping in reactions

MDL Formats
^^^^^^^^^^^

MDL (Symyx) Molfiles and Rxnfiles are supported by Bingo. Both format
versions (2000 and 3000) are supported. Almost all format features are
supported, including:

-  Pseudo-atoms (atom aliases)
-  Stereogroups
-  R-Groups (Markush queries)
-  Query atoms and query bonds
-  Various query flags on atoms and bonds
-  Atom positions
-  3D constraints in v2000 Molfiles
-  Reaction atom-to-atom mapping (AAM)
-  Reacting centers and stereo inv/ret flags

The only features that are not supported are:

-  SGroups and polymers
-  3D constraints in v3000 Molfiles

MDL (Symyx) SDfile format (.sdf) is supported for export from user
tables. SDFile, RDfile (.rdf), and multiline SMILES formats are
supported for import to user tables.

Internal Binary Formats
^^^^^^^^^^^^^^^^^^^^^^^

Internal Bingo binary molecule and reaction formats are designed
exclusively for database molecules and reactions, but not for queries.
All the molecule and reaction features that are not query features are
supported, including:

-  Pseudo-atoms
-  Aromatic rings
-  Tetrahedral stereocenters, allene stereo, stereogroups, and cis-trans
   double bonds
-  Reaction atom-to-atom mapping (AAM)
-  Reacting centers and stereo inv/ret flags
-  Atom positions (optional)
