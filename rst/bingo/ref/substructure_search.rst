Description and Syntax
^^^^^^^^^^^^^^^^^^^^^^

The general form of substructure search query is as follows:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, $parameters)=1;

-  ``$table`` is the name of the table containing molfile CLOBs in the
   column ``$column``.
-  ``$query`` is a VARCHAR2 or CLOB containing the query molfile or
   SMILES string.
-  ``$parameters`` is a VARCHAR2 string.

You can omit the ``$parameters`` value:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query)=1;

This is equal to the following:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, '')=1;

A substructure search query with no ``$parameters`` returns the
molecules that include the query structure as the substructure or exact
match. The matched part is highlighted in examples.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image2|             | |image3|                          |
+----------------------+-----------------------------------+

The query molecule can be disconnected. Matched fragments in the target
structure cannot overlap.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image7|             | |image8|                          | |image9|                              |
+----------------------+-----------------------------------+---------------------------------------+

Substructure Query Features
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Explicit Hydrogens
''''''''''''''''''

The explicit hydrogens specified in the query structure must match any
(explicit or implicit) hydrogen in the target structure.

+-------------------------+-------------------------+-------------------------+
| Substructure Query      | Examples of Molecules   | Examples of Molecules   |
|                         | Retrieved               | Not Retrieved           |
+=========================+=========================+=========================+
| |image18|               | |image19|               | |image20|               |
+-------------------------+-------------------------+-------------------------+
| |image21|               | |image22|               | |image23|               |
+-------------------------+-------------------------+-------------------------+
| |image24|               | |image25|               |                         |
+-------------------------+-------------------------+-------------------------+

Charges and Radicals
''''''''''''''''''''

The presence of charged atoms in the query molecule is an additional
property. If the charge is specified, it must match the charge in the
target molecule. An atom without a specific charge can match an atom
with either charge. The same rule applies for radicals.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image35|            | |image36|                         | |image37|                             |
+----------------------+-----------------------------------+---------------------------------------+
| |image38|            | |image39|                         | |image40|                             |
+----------------------+-----------------------------------+---------------------------------------+
| |image41|            | |image42|                         | |image43|                             |
+----------------------+-----------------------------------+---------------------------------------+

Isotopes
''''''''

The presence of isotopes atoms in the query molecule is an additional
property, like charges.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image48|            | |image49|                         |
+----------------------+-----------------------------------+
| |image50|            | |image51|                         |
+----------------------+-----------------------------------+

Valence
'''''''

Valence can be specified on the query atoms.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image55|            | |image56|                         | |image57|                             |
+----------------------+-----------------------------------+---------------------------------------+

Preventing Hydrogen Substitutions
'''''''''''''''''''''''''''''''''

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image61|            | |image62|                         | |image63|                             |
+----------------------+-----------------------------------+---------------------------------------+

Number of Non-Hydrogen Substitutions
''''''''''''''''''''''''''''''''''''

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image67|            | |image68|                         | |image69|                             |
+----------------------+-----------------------------------+---------------------------------------+

Unsaturation flag
'''''''''''''''''

An unsaturated atom must have at least one non-single bond.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image73|            | |image74|                         | |image75|                             |
+----------------------+-----------------------------------+---------------------------------------+

Ring Bond Count
'''''''''''''''

You can specify the number of ring bonds that are connected to the atom.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image79|            | |image80|                         | |image81|                             |
+----------------------+-----------------------------------+---------------------------------------+

Bond Topology
'''''''''''''

“Ring” query bonds must match the ring(s) of the target molecule;
“chain” query bonds must not.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image88|            | |image89|                         | |image90|                             |
+----------------------+-----------------------------------+---------------------------------------+
| |image91|            | |image92|                         | |image93|                             |
+----------------------+-----------------------------------+---------------------------------------+

Query Atom Labels
'''''''''''''''''

“A” query atom matches any atom except hydrogen (or its isotopes). “Q”
query atom matches any atom except hydrogen and carbon.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image100|           | |image101|                        | |image102|                            |
+----------------------+-----------------------------------+---------------------------------------+
| |image103|           | |image104|                        | |image105|                            |
+----------------------+-----------------------------------+---------------------------------------+

Atom Lists
''''''''''

You can specify the list of elements that are allowed or prohibited for
the query atom. Hydrogen in the list can match the explicit or implicit
hydrogen of the target.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image110|           | |image111|                        |
+----------------------+-----------------------------------+
| |image112|           | |image113|                        |
+----------------------+-----------------------------------+

Query Bonds
'''''''''''

The following types of query bonds are supported:

-  Single or double
-  Single or aromatic
-  Double or aromatic
-  Any

Below is an example with 'Single or Double' bonds. Such bonds cannot
match aromatic target bonds.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image117|           | |image118|                        | |image119|                            |
+----------------------+-----------------------------------+---------------------------------------+

Cis-trans Isomerism
^^^^^^^^^^^^^^^^^^^

You can specify the “stereo” flag on a carbon double bond that you do
not want to rotate in order to exclude cis-trans isomers from the search
results. Explicit and implicit hydrogen substituents are supported.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image126|           | |image127|                        | |image128|                            |
+----------------------+-----------------------------------+---------------------------------------+
| |image129|           | |image130|                        | |image131|                            |
+----------------------+-----------------------------------+---------------------------------------+

Chirality
^^^^^^^^^

The following tetrahedral stereocenters are allowed:

-  C or Si or N+ with 3 single bonds (implicit hydrogen)
-  C or Si or N+ with 4 single bonds
-  S with 2 single bonds and 2 double bonds
-  P with 3 single bonds and 1 double bond
-  P+ with 4 single bonds

Also, a special type of tetrahedral stereocenter—with the pyramid is
formed by 3 neighbor atoms and the lone pair of electrons—is allowed:

-  N or P or S+ with 3 single bonds
-  S with 2 single bonds and 1 double bond

The stereocenter is defined by up- or down-oriented stereobond(s)
connected to it. The chirality is determined from the stereobond
orientation and the position of atoms. The stereocenter that has an
“absolute” configuration can match only “absolute” stereocenters that
have the same chirality.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image135|           | |image136|                        | |image137|                            |
+----------------------+-----------------------------------+---------------------------------------+

Here are two examples of non-carbon chiral centers:

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image142|           | |image143|                        |
+----------------------+-----------------------------------+
| |image144|           | |image145|                        |
+----------------------+-----------------------------------+

MDL notation of stereogroups is supported. “AND” stereocenters can match
“AND”, “OR”, and absolute ones; “OR” stereocenters can match “OR” and
absolute ones. Target stereo-groups cannot be more fragmented than the
query stereo-groups.

+-------------------------+-------------------------+-------------------------+
| Substructure Query      | Examples of Molecules   | Examples of Molecules   |
|                         | Retrieved               | Not Retrieved           |
+=========================+=========================+=========================+
| |image151|              | |image152|              | |image153|              |
+-------------------------+-------------------------+-------------------------+
| |image154|              | |image155|              |                         |
+-------------------------+-------------------------+-------------------------+

“Either” stereobond can be specified in the query. The corresponding
stereocenter matches any stereocenter regardless of chirality.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image159|           | |image160|                        | |image161|                            |
+----------------------+-----------------------------------+---------------------------------------+

**Note:** The embedding of the substructure is not limited to the way in
which it is drawn. Sometimes, single bonds can “swap”, producing the
hits that are correct, but appear strange.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image164|           | |image165|                        |
+----------------------+-----------------------------------+

**Note:** A chiral center with explicit hydrogen can match a chiral
center with implicit hydrogen, and vice versa.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image170|           | |image171|                        |
+----------------------+-----------------------------------+
| |image172|           | |image173|                        |
+----------------------+-----------------------------------+

Markush Search
^^^^^^^^^^^^^^

Markush search has the same syntax as the basic substructure search, and
it will be performed automatically if the query molecule contains one or
more R-groups.

+-----------------+-----------------------------------+---------------------------------------+
| Markush Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+=================+===================================+=======================================+
| |image180|      | |image181|                        | |image182|                            |
+-----------------+-----------------------------------+---------------------------------------+
| |image183|      | |image184|                        | |image185|                            |
+-----------------+-----------------------------------+---------------------------------------+

Aromaticity in Substructure Search and Markush Search
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Basic Queries
'''''''''''''

Aromatic bonds can match only aromatic bonds.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image195|           | |image196|                        | |image197|                            |
+----------------------+-----------------------------------+---------------------------------------+
| |image198|           | |image199|                        | |image200|                            |
+----------------------+-----------------------------------+---------------------------------------+
| |image201|           | |image202|                        | |image203|                            |
+----------------------+-----------------------------------+---------------------------------------+

Queries with Query Features
'''''''''''''''''''''''''''

Some queries with query features can have ambiguous aromaticity status:
they are aromatic in one matching and not aromatic in another matching.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image210|           | |image211|                        | |image212|                            |
+----------------------+-----------------------------------+---------------------------------------+
| |image213|           | |image214|                        | |image215|                            |
+----------------------+-----------------------------------+---------------------------------------+

Aromaticity and Markush Search
''''''''''''''''''''''''''''''

Markush queries are allowed to match both aromatic and non-aromatic
targets.

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image218|           | |image219|                        |
+----------------------+-----------------------------------+

Charge and Aromaticity
''''''''''''''''''''''

Charges and aromatic bonds are matched independently. In some structures
where the acquisition of the charge by an atom destroys the aromaticity
of a ring, matching is not possible due to the mismatch of bond orders.

+----------------------+-------------------------------------------+
| Substructure Query   | Examples of Molecules **Not** Retrieved   |
+======================+===========================================+
| |image222|           | |image223|                                |
+----------------------+-------------------------------------------+

However, uncharged aromatic queries match charged aromatic structures:

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image226|           | |image227|                        |
+----------------------+-----------------------------------+

Pseudo-atoms
^^^^^^^^^^^^

Pseudo-atom in the query structure can match only the same pseudo-atom
in the target structure. The matching is case-sensitive.

+----------------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===================================+=======================================+
| |image231|           | |image232|                        | |image233|                            |
+----------------------+-----------------------------------+---------------------------------------+

Pseudo-atoms in target structures are never expanded:

+----------------------+---------------------------------------+
| Substructure Query   | Examples of Molecules Not Retrieved   |
+======================+=======================================+
| |image236|           | |image237|                            |
+----------------------+---------------------------------------+

Query atoms can match pseudo-atoms:

+----------------------+-----------------------------------+
| Substructure Query   | Examples of Molecules Retrieved   |
+======================+===================================+
| |image240|           | |image241|                        |
+----------------------+-----------------------------------+

**Note:** 'X' atom is treated as 'any halogen' query atom by default,
but there is an option to treat it as pseudo-atom. In order to treat it
so, please run the following SQL statement prior to table indexing:

::

    exec Bingo.TreatXAsPseudoatom(1);

After that, please reconnect to the database. This setting will be
saved, so you will never need to run the statement again (unless you
re-install the cartridge). To get the original behavior back, you can
run the following SQL statement:

::

    exec Bingo.TreatXAsPseudoatom(0);

+----------------------+--------------------------------------------+-------------------------------------------------------------------+
| Substructure Query   | Examples of Molecules Retrieved (Or Not)   | Comment                                                           |
+======================+============================================+===================================================================+
| |image246|           | |image247|                                 | Matches with “x as pseudo atom” option;                           |
|                      |                                            |  Raises an error with “x as any halogen atom” option (default).   |
+----------------------+--------------------------------------------+-------------------------------------------------------------------+
| |image248|           | |image249|                                 | Matches with “x as any halogen atom” option (default);            |
|                      |                                            |  Does not match with “x as pseudo atom” option.                   |
+----------------------+--------------------------------------------+-------------------------------------------------------------------+

Resonance Search
^^^^^^^^^^^^^^^^

The resonance substructure search is provided by the ``Sub`` operator
with ``RES`` parameter:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, 'RES')=1;

With this type of search you can find molecules whose resonance forms
contain the query molecule.

+----------------------+---------------------------------+--------------------------+
| Substructure Query   | Example of Molecule Retrieved   | Matched Resonance Form   |
+======================+=================================+==========================+
| |image256|           | |image257|                      | |image258|               |
+----------------------+---------------------------------+--------------------------+
| |image259|           | |image260|                      | |image261|               |
+----------------------+---------------------------------+--------------------------+

The query molecule can contain any query features:

+----------------------+---------------------------------+--------------------------+
| Substructure Query   | Example of Molecule Retrieved   | Matched Resonance Form   |
+======================+=================================+==========================+
| |image268|           | |image269|                      | |image270|               |
+----------------------+---------------------------------+--------------------------+
| |image271|           | |image272|                      | |image273|               |
+----------------------+---------------------------------+--------------------------+

Impossible resonance forms are not matched:

+----------------------+-------------------------------------+
| Substructure Query   | Example of Molecule Not Retrieved   |
+======================+=====================================+
| |image276|           | |image277|                          |
+----------------------+-------------------------------------+

Actually, only the *main resonance contributors* are matched. The main
resonance contributors are resonance forms that have the maximum number
of atoms with the full octet and/or the minimum number of atoms with
nonzero formal charge. For example, the following structure would not
match itself because both atoms are charged and only one atom has a full
octet:

+----------------------+-------------------------------------+
| Substructure Query   | Example of Molecule Not Retrieved   |
+======================+=====================================+
| |image280|           | |image281|                          |
+----------------------+-------------------------------------+

Uncharged atoms still match charged ones in the resonance search:

+----------------------+---------------------------------+--------------------------+
| Substructure Query   | Example of Molecule Retrieved   | Matched Resonance Form   |
+======================+=================================+==========================+
| |image285|           | |image286|                      | |image287|               |
+----------------------+---------------------------------+--------------------------+

A resonance chain can be of any length:

+----------------------+---------------------------------+
| Substructure Query   | Example of Molecule Retrieved   |
+======================+=================================+
| |image290|           | |image291|                      |
+----------------------+---------------------------------+

Cyclic resonance forms are currently not supported:

+----------------------+-------------------------------------+
| Substructure Query   | Example of Molecule Not Retrieved   |
+======================+=====================================+
| |image294|           | |image295|                          |
+----------------------+-------------------------------------+

3D Constraints
^^^^^^^^^^^^^^

Bingo supports all types of 3D constraints for the queries in MDL
(Symyx) Molfile 2000 format:

-  Distance ranges
-  Angle ranges
-  Dihedral angle ranges
-  Exclusion spheres

The substructure match with 3D constraints follows the rules of the
ordinary substructure match. In addition, the 3D constraints defined in
the query molecule must be fulfilled by the corresponding atoms of the
target. If the query can be embedded in several ways, all embeddings are
checked. The query matches the target when at least one embedding
conforms to the conditions.

**Note:** 3D constraints of Molfile 3000 format are not supported.

Affine Transformation Search
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This type of 3D search treats the molecule as a rigid structure
consisting of points in space. Similar to the case of the search with
constraints, all inclusions of the query are checked against the
following condition: the structure of the query is transformed to its
image on the target by an affine transformation
(translation+rotation+scale). 1 The syntax of the affine transformation
substructure search is as follows:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, 'AFF $rms')=1;

``rms`` is the maximum allowed root-mean-square deviation of all imposed
atoms. It is measured in angstroms.

The query atoms that are fixed must be labeled fixed. The imposition of
other atoms is not restricted to ``rms``.

The following example makes no chemical sense, but is included here as a
simple two-dimensional illustration of the affine transformation search:

+----------------------+---------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Parameters    | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+===============+===================================+=======================================+
| |image299|           | ``AFF 0.1``   | |image300|                        | |image301|                            |
+----------------------+---------------+-----------------------------------+---------------------------------------+

**Note:** When no atoms are labeled fixed, all of them are considered
fixed.

Conformational Search
^^^^^^^^^^^^^^^^^^^^^

Any conformation can be obtained by rotating the molecule around single
bonds. Thus, the inclusion is correct if the image of the query molecule
is the conformation of the query, i.e. a sequence of rotations of the
molecule around single bonds converts the query into a substructure of
the target. In a way similar to affine transformation search, you can
set the ``rms`` parameter in order to define the accuracy of the
transformation.

The syntax of the conformational substructure search is as follows:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, 'CONF $rms')=1;

+----------------------+----------------+-----------------------------------+---------------------------------------+
| Substructure Query   | Parameters     | Examples of Molecules Retrieved   | Examples of Molecules Not Retrieved   |
+======================+================+===================================+=======================================+
| |image305|           | ``CONF 0.1``   | |image306|                        | |image307|                            |
+----------------------+----------------+-----------------------------------+---------------------------------------+
