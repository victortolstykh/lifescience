Description and Syntax
^^^^^^^^^^^^^^^^^^^^^^

This type of search estimates the similarity of the molecules by
comparing their bit imprints (fingerprints). Characteristics based on
the following metrics are supported:

-  Tanimoto metric: c / (a + b - c)
-  Tversky metric: c / (alpha \* (a-c) + beta \* (b-c) + c)
-  Euclidean metric for substructures: c / a

where

-  a is the count of bits in the fingerprint of the query
-  b is the count of bits in the fingerprint of the target
-  c is the count of coincident bits in the fingerprints

All characteristics have values from 0 to 1, with the value of 1
providing the maximum similarity (which means equal fingerprints).

You can specify in the query the minimum similarity and/or the maximum
similarity that the fetched molecules must have.

::

    SELECT * FROM $table WHERE Bingo.Sim($column, $query, $metric) > $min;

    SELECT * FROM $table WHERE Bingo.Sim($column, $query, $metric) < $max;

    SELECT * FROM $table WHERE Bingo.Sim($column, $query, $metric) BETWEEN $min AND $max;

-  ``$min`` is the lower limit of the desired similarity.
-  ``$max`` is the upper limit.
-  ``$metric`` is a string specifying the metric to use: ``tanimoto`` ,
   ``tversky``, or ``euclid-sub``. In case of Tversky metric, there are
   optional "alpha" and "beta" parameters: ``tversky 0.9 0.1`` denotes
   alpha = 0.9, beta = 0.1. The default is alpha = beta = 0.5 (Dice
   index).

You can omit the ``$metric`` parameter and write
``Bingo.Sim($column, $query)``. The default Tanimoto metric will be
used.

**Note:** Query features are not allowed in query molecules for
similarity search.

Examples
^^^^^^^^

+------------------+----------------------------+---------------+-----------------------------------+
| Query Molecule   | Metrics                    | Lower Limit   | Examples of Molecules Retrieved   |
+==================+============================+===============+===================================+
| |image370|       | Tanimoto                   | 0.7           | |image371|                        |
+------------------+----------------------------+---------------+-----------------------------------+
| |image372|       | Euclid for Substructures   | 0.95          | |image373|                        |
+------------------+----------------------------+---------------+-----------------------------------+
