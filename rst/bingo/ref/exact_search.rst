The general form of exact search query is as follows:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, $parameters)=1;

You can omit the ``$parameters`` value:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query)=1;

It is equal to:

::

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, 'ALL')=1;

This kind of search makes it possible for you to set various search
conditions. If no search conditions are set, two molecules are
considered similar when they are completely equal (up to aromaticity and
implicit/explicit hydrogens). You can set up the flags to match only
some characteristics of the molecule:

The supported flags are:

+------------+------------------------------------------------------------------------------+
| Flag       | Comment                                                                      |
+============+==============================================================================+
| ELE        | Distribution of electrons: bond types, atom charges, radicals, valences      |
+------------+------------------------------------------------------------------------------+
| MAS        | Atom isotopes                                                                |
+------------+------------------------------------------------------------------------------+
| STE        | Stereochemistry: chiral centers, stereogroups, and cis-trans bonds           |
+------------+------------------------------------------------------------------------------+
| FRA        | Connected fragments: disallows match of separate ions in salts               |
+------------+------------------------------------------------------------------------------+
| ALL        | All of the above (the most restrictive kind of search)                       |
+------------+------------------------------------------------------------------------------+
| NONE       | None of the above (the most flexible kind of search)                         |
+------------+------------------------------------------------------------------------------+
| ``$rms``   | Affine transformation, see the substructure search description for details   |
+------------+------------------------------------------------------------------------------+

The flags, which can be combined in any way, should go in the parameters
string separated by space. The ``rms`` number, if present, should go
after the flags; for example: ``ALL 0.1``. You can write the minus sign
before the flag to exclude it from the 'ALL' flag. For example, 'ALL
-MAS' means that all the described features except the isotopes must
match. The ``NONE`` flag, if present, must be single.

+----------------------+------------------------------------------+---------------------------------------------------------------+
| Exact Search Query   | Example of Molecule Retrieved (or Not)   | Comment                                                       |
+======================+==========================================+===============================================================+
| |image319|           | |image320|                               | Matches with 'ALL -MAS', does not match with 'ALL' or 'MAS'   |
+----------------------+------------------------------------------+---------------------------------------------------------------+
| |image321|           | |image322|                               | Matches with 'ALL -ELE', does not match with 'ALL' or 'ELE'   |
+----------------------+------------------------------------------+---------------------------------------------------------------+
| |image323|           | C                                        | Matches with 'ALL'                                            |
+----------------------+------------------------------------------+---------------------------------------------------------------+
| |image324|           | |image325|                               | Matches with 'ALL -FRA', does not match with 'ALL' or 'FRA'   |
+----------------------+------------------------------------------+---------------------------------------------------------------+
| |image326|           | |image327|                               | Matches with 'ALL -STE', does not match with 'ALL' or 'STE'   |
+----------------------+------------------------------------------+---------------------------------------------------------------+
| |image328|           | |image329|                               | Matches with 'ALL', does not match with '0.1' or 'ALL 0.1'    |
+----------------------+------------------------------------------+---------------------------------------------------------------+

On aromatic molecules, the ``BON`` flag is not sensitive to the
difference between single and double bonds that form the aromatic rings.

+----------------------+---------------------------------+----------------------+
| Exact Search Query   | Example of Molecule Retrieved   | Comment              |
+======================+=================================+======================+
| |image332|           | |image333|                      | Matches with 'ALL'   |
+----------------------+---------------------------------+----------------------+

**Note:** Query features are not allowed in exact search.
