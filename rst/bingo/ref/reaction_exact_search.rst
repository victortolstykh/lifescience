The general form of reaction exact search query is as follows:

::

    SELECT * FROM $table WHERE Bingo.RExact($column, $query, $parameters)=1;

You can omit the ``$parameters`` value:

::

    SELECT * FROM $table WHERE Bingo.RExact($column, $query)=1;

It is equal to:

::

    SELECT * FROM $table WHERE Bingo.RExact($column, $query, 'ALL')=1;

This kind of search makes it possible for you to set various search
conditions. If no search conditions are set, two molecules are
considered similar when they are completely equal (up to aromaticity and
implicit/explicit hydrogens). You can set up the flags to match only
some characteristics of the molecule:

The supported flags are:

+--------+---------------------------------------------------------------------------+
| Flag   | Comment                                                                   |
+========+===========================================================================+
| ELE    | Distribution of electrons: bond types, atom charges, radicals, valences   |
+--------+---------------------------------------------------------------------------+
| MAS    | Atom isotopes                                                             |
+--------+---------------------------------------------------------------------------+
| STE    | Stereochemistry: chiral centers, stereogroups, and cis-trans bonds        |
+--------+---------------------------------------------------------------------------+
| AAM    | Atom-to-atom mapping                                                      |
+--------+---------------------------------------------------------------------------+
| RCT    | Reacting centers                                                          |
+--------+---------------------------------------------------------------------------+
| ALL    | All of the above (the most restrictive kind of search)                    |
+--------+---------------------------------------------------------------------------+
| NONE   | None of the above (the most flexible kind of search)                      |
+--------+---------------------------------------------------------------------------+

The flags, which can be combined in any way, should go in the parameters
string separated by space. You can write the minus sign before the flag
to exclude it from the 'ALL' flag. For example, 'ALL -MAS -AAM' means
that all the described features except the isotopes and the AAM numbers
must match. The ``NONE`` flag, if present, must be single.
