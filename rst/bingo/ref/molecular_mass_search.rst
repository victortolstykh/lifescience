Description and syntax
^^^^^^^^^^^^^^^^^^^^^^

The ``Bingo.Mass`` operator returns molecular mass as the sum of the
standard atomic weights for atoms without isotope specified and relative
atomic masses of isotopes. The table with masses was extracted from the
http://physics.nist.gov/PhysRefData/Compositions website.

::

    SELECT Bingo.Mass($molecule) FROM DUAL;

    SELECT Bingo.Mass($column) FROM $table;

You can also query a table for the molecules with molecular mass more
than a value, less than a value, or between two values.

::

    SELECT * FROM $table WHERE Bingo.Mass($column) > $lower;

    SELECT * FROM $table WHERE Bingo.Mass($column) < $upper;

    SELECT * FROM $table WHERE Bingo.Mass($column) BETWEEN $lower AND $upper;

Examples
^^^^^^^^

+----------------------------------+-----------------------------------+-----------+
| Query                            | Examples of Molecules Retrieved   | Mass      |
+==================================+===================================+===========+
| ``Bingo.Mass(molecule) > 100``   | |image382|                        | 130.185   |
+----------------------------------+-----------------------------------+-----------+
| ``Bingo.Mass(molecule) < 100``   | |image383|                        | 94.115    |
+----------------------------------+-----------------------------------+-----------+

Customization
^^^^^^^^^^^^^

Bingo provides the possibility for changing default atom masses with the
following procedure:

::

    EXECUTE BEGIN Bingo.SetRelativeAtomicMass($str); END;

``$str`` is the VARCHAR2 string. Its value must be contain the default
atom masses separated by semicolons, for example:
”\ ``C 12; N 14; O 16``\ ”.

Other Kinds of Molecular Weight
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``Bingo.Mass`` has an optional ``VARCHAR2`` parameter, which defines
the 'kind' of the resulting molecular mass value:

-  ``Bingo.Mass($molecule, 'molecular-weight')`` returns the molecular
   weight (this is the default).
-  ``Bingo.Mass($molecule, 'most-abundant-mass')`` returns the `most
   abundant
   mass <http://en.wikipedia.org/wiki/Mass%20%28mass%20spectrometry%29#Most%20abundant%20mass#Most%20abundant%20mass>`__,
   which is calculated using most likely isotopic composition for a
   single random molecule.
-  ``Bingo.Mass($molecule, 'monoisotopic-mass')`` returns the
   `monoisotopic
   mass <http://en.wikipedia.org/wiki/Monoisotopic_mass>`__, which is
   calculated using the most abundant isotope of each element.
