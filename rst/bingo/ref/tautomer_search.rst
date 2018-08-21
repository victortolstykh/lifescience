Syntax
^^^^^^

The general form of exact tautomer search query is the following:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, $parameters)=1;

The general form of tautomer substructure search query is the following:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, $parameters)=1;

for tautomer-as-substructure search

-  ``$table`` is the name of the table containing molfile CLOBs in the
   column ``$column``.
-  ``$query`` is a VARCHAR2 or CLOB containing the query molfile or
   SMILES string.
-  ``$parameters`` is a VARCHAR2 containing parameters that restrict the
   resulting set of molecules by various criteria.

The ``$parameters`` string must begin with the ``TAU`` word. If it is
the only word, the search with the less restriction will be performed:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'TAU')=1;

Some metal bonds and atom charges can replace hydrogen in tautomeric
chains. You can add the ``HYD`` word to disable such hydrogen
replacements:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'TAU HYD')=1;

Ring-chain tautomerism is disabled by default. You can add ``R-C``
string parameter to enable it.

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'TAU R-C')=1;

**Note:** The support of the ring-chain tautomerism is experimental and
may not work properly.

Also you can restrict the tautomer search by enabling conditions for
boundary atoms in tautomeric chains. By default, there are three
conditions:

#. Each boundary atom in the tautomeric chain must be one of ``N``,
   ``O``, ``P``, ``S``, ``As``, ``Se``, ``Sb``, ``Te``
#. Carbon not from the aromatic ring at one end of the tautomeric chain,
   and one of ``N``, ``O``, ``P``, ``S`` at the other end
#. Carbon from the aromatic ring at one end of the tautomeric chain and
   one of ``N``, ``O`` at the other end

To enable the first condition put ``R1`` to ``$parameters`` string
(``R2`` to enable the second condition, ``R3`` to enable the third
condition):

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'TAU R1 R3')=1;

If you want all conditions enabled, just put ``R*``:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'TAU R*')=1;

Each tautomeric chain is checked to conform to one of the given rules.
The more rules you specify, the more flexibility you receive in the
search; *but* when you specify no rules at all (``TAU``), you get the
most flexible search because no rules are checked. Any tautomeric chain
is acceptable in this case.

Exact Tautomer Search
^^^^^^^^^^^^^^^^^^^^^

The resulting set of this kind of search can contain exact matches.

+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+
| Tautomer Query   | Examples of Molecules Retrieved (or Not)   | Comment                                                                                    |
+==================+============================================+============================================================================================+
| |image344|       | |image345|                                 | Matches with ``TAU`` or ``TAU R2``, does not match with ``TAU R1 R3``                      |
+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+
| |image346|       | |image347|                                 | Matches with ``TAU R-C`` or ``TAU R-C R2``, does not match with ``TAU`` or ``TAU R1 R3``   |
+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+
| |image348|       | |image349|                                 | Matches with ``TAU`` or ``TAU R1``, does not match with ``TAU R2 R3``                      |
+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+
| |image350|       | |image351|                                 | Matches with ``TAU`` or ``TAU R1``, does not match with ``TAU R2 R3``                      |
+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+
| |image352|       | |image353|                                 | Matches with ``TAU``, does not match with ``TAU R*``                                       |
+------------------+--------------------------------------------+--------------------------------------------------------------------------------------------+

**Note:** The retrieved molecules in the first row are completely the
same because of their aromaticity.

Tautomer Substructure Search
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The resulting set of this kind of search can contain exact tautomer
matches. Additional tautomer parameters have the same effect as in the
exact tautomer search.

+------------------+--------------------------------------------+-------------------------------------------------------------------------+
| Tautomer Query   | Examples of Molecules Retrieved (or Not)   | Comment                                                                 |
+==================+============================================+=========================================================================+
| |image360|       | |image361|                                 | Matches with ``TAU`` or ``TAU R1``, does not match with ``TAU R2 R3``   |
+------------------+--------------------------------------------+-------------------------------------------------------------------------+
| |image362|       | |image363|                                 | Matches with ``TAU`` or ``TAU R2``, does not match with ``TAU R1 R3``   |
+------------------+--------------------------------------------+-------------------------------------------------------------------------+
| |image364|       | |image365|                                 | Matches with ``TAU``, does not match with ``TAU R*``                    |
+------------------+--------------------------------------------+-------------------------------------------------------------------------+

Customizing the Rules
^^^^^^^^^^^^^^^^^^^^^

``Bingo`` user has a table called ``TAUTOMER_RULES``. The three rules
defined above are contained in this table:

::

    SELECT * FROM Bingo.TAUTOMER_RULES;

       ID                  BEG                  END
    -----  -------------------  -------------------
        1  N,O,P,S,As,Se,Sb,Te  N,O,P,S,As,Se,Sb,Te
        2                   0C              N,O,P,S
        3                   1C                  N,O

You can add, remove or update the defined rules. VARCHAR2 strings
``BEG`` and ``END`` refer to the ends of the tautomeric chain. Allowed
elements are separated by commas. '1' at the beginning means an aromatic
atom, and '0' means an aliphatic (non-aromatic) atom.

::

    INSERT INTO Bingo.TAUTOMER_RULES values($id, $beg, $end);

**Note:** The ID numbers must be different and belong to the range from
1 to 32.

Tautomer Substructure Search Based on InChI or reaction SMARTS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This type of tautomer search is based on the tautomer enumeration procedure using one of supported methods (InChI or RSMARTS).

The query syntax is the following (for InChI):

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, 'TAU INCHI')=1;

And for reaction SMARTS:
::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, 'TAU RSMARTS')=1;

The output depends on the set of tautomers found by the selected enumeration procedure. For example for the following molecule/query the output differs:

.. indigorenderer::
    :indigoobjecttype: code
    :indigoloadertype: code
    :nocode:

    molecule = indigo.loadMolecule('OC1C2C=NNC=2N=CN=1')
    query = indigo.loadQueryMolecule("O=CCCN")
    molecule.setProperty("grid-comment", "Molecule")
    query.setProperty("grid-comment", "Query")
    array = indigo.createArray()
    array.arrayAdd(molecule)
    array.arrayAdd(query)

    indigo.setOption("render-grid-margins", "20, 10")
    indigo.setOption("render-grid-title-font-size", "10")
    indigo.setOption("render-grid-title-property", "grid-comment")
    indigoRenderer.renderGridToFile(array, None, 2, 'result.png')


Below is the set of possible tautomers for ``INCHI`` option and query mappings:

.. indigorenderer::
    :indigoobjecttype: code
    :indigoloadertype: code
    :nocode:

    molecule = indigo.loadMolecule('OC1C2C=NNC=2N=CN=1')

    iter = indigo.iterateTautomers(molecule, 'INCHI')
    array = indigo.createArray()
    for imol in iter:
        mol = imol.clone()
        array.arrayAdd(mol)

    indigo.setOption("render-bond-length", "20")
    indigo.setOption("render-grid-margins", "20, 10")
    indigoRenderer.renderGridToFile(array, None, 5, 'result.png')

.. indigorenderer::
    :indigoobjecttype: code
    :indigoloadertype: code
    :nocode:

    molecule = indigo.loadMolecule('OC1C2C=NNC=2N=CN=1')
    query = indigo.loadQueryMolecule("O=CCCN")
    matcher = indigo.substructureMatcher(molecule, "TAU INCHI")
    matches = matcher.iterateMatches(query)
    array = indigo.createArray()
    for mapping in matches:
        array.arrayAdd(mapping.highlightedTarget())

    indigo.setOption("render-highlight-color", "0, 0, 1")
    indigo.setOption("render-highlight-thickness-enabled", "True")
    indigoRenderer.renderGridToFile(array, None, 4, 'result.png')

The result for ``RSMARTS`` option (same molecule and query):

.. indigorenderer::
    :indigoobjecttype: code
    :indigoloadertype: code
    :nocode:

    molecule = indigo.loadMolecule('OC1C2C=NNC=2N=CN=1')

    iter = indigo.iterateTautomers(molecule, 'RSMARTS')
    array = indigo.createArray()
    for imol in iter:
        mol = imol.clone()
        array.arrayAdd(mol)

    indigo.setOption("render-bond-length", "20")
    indigo.setOption("render-grid-margins", "20, 10")
    indigoRenderer.renderGridToFile(array, None, 5, 'result.png')

.. indigorenderer::
    :indigoobjecttype: code
    :indigoloadertype: code
    :nocode:

    molecule = indigo.loadMolecule('OC1C2C=NNC=2N=CN=1')
    query = indigo.loadQueryMolecule("O=CCCN")
    matcher = indigo.substructureMatcher(molecule, "TAU RSMARTS")
    matches = matcher.iterateMatches(query)
    array = indigo.createArray()
    for mapping in matches:
        array.arrayAdd(mapping.highlightedTarget())

    indigo.setOption("render-highlight-color", "0, 0, 1")
    indigo.setOption("render-highlight-thickness-enabled", "True")
    indigoRenderer.renderGridToFile(array, None, 4, 'result.png')
