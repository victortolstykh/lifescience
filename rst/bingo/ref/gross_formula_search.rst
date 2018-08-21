
Description and Syntax
^^^^^^^^^^^^^^^^^^^^^^

You can get the gross formula of the molecule with the ``Bingo.Gross()``
operator:

::

    SELECT Bingo.Gross($molfile) FROM DUAL;

    SELECT Bingo.Gross('C1C=CC=CC=1') FROM DUAL;

    SELECT Bingo.Gross($column) FROM $table;

You can also query a table for molecules with gross formula more than,
less than, or equal to query gross formula.

::

    SELECT * FROM $table WHERE Bingo.Gross($column, '>= $query')=1;

    SELECT * FROM $table WHERE Bingo.Gross($column, '<= $query')=1;

    SELECT * FROM $table WHERE Bingo.Gross($column, '= $query')=1;

The order of atoms and the spaces in the query does not matter.

+-------------+------------+--------------+
| Left Side   | Relation   | Right Side   |
+=============+============+==============+
| OC6         | =          | C6 O         |
+-------------+------------+--------------+
| OC6         | ?          | C6 O         |
+-------------+------------+--------------+
| C6 O        | ?          | C8 O2        |
+-------------+------------+--------------+
| C6 Cl       | ?          | C6           |
+-------------+------------+--------------+
| C6 H5       | ?          | C6 H6        |
+-------------+------------+--------------+

**Note:** Gross formula are not always comparable: for example, ‘C2 H6
O’ and ‘Ag O N C’

Examples
^^^^^^^^

+------------------+-----------------------------------+
| Query            | Examples of Molecules Retrieved   |
+==================+===================================+
| ``= C6 H6``      | |image377|                        |
+------------------+-----------------------------------+
| ``<= C4 H4 O``   | |image378|                        |
+------------------+-----------------------------------+
| ``>= Cl6``       | |image379|                        |
+------------------+-----------------------------------+
