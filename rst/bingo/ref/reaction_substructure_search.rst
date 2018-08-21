Description and Syntax
^^^^^^^^^^^^^^^^^^^^^^

The general form of the substructure search query is the following:

::

    SELECT * FROM $table WHERE Bingo.RSub($column, $query)=1;

-  ``$table`` is the name of the table containing the reaction
   ``$column``. The target reactions may be represented in Rxnfile,
   reaction SMILES or binary format. ``$column`` may have CLOB,
   VARCHAR2, and BLOB data type.
-  ``$query`` is a VARCHAR2 or CLOB containing the query Rxnfile or
   reaction SMILES.

Examples
^^^^^^^^

You can specify an arbitrary amount of reactants and products in the
query. The different reactants/products of the query match the different
reactants/products of the matched target.

Reaction Substructure Query

|image384|

Example of Reaction Retrieved

|image385|

You can specify an empty reactant or empty target:

Reaction Substructure Query

|image386|

Example of Reaction Retrieved

|image387|

Query atom-to-atom mapping, when present, is taken into account:

Reaction Substructure Query

|image388|

Example of Reaction Retrieved

|image389|

Example of Reaction Not Retrieved

|image390|

Reacting centers in the query, if present, match the target reacting
centers as well:

Reaction Substructure Query

|image391|

Example of Reaction Retrieved

|image392|

Example of Reaction Not Retrieved

|image393|

Stereo inversion/retention flags are supported in the query:

Reaction Substructure Query

|image394|

Example of Reaction Retrieved

|image395|

Example of Reaction Not Retrieved

|image396|

You can specify any query features, as in the molecule substructure
search, except the R-Groups:

Reaction Substructure Query

|image397|

Example of Reaction Retrieved

|image398|
