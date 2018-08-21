Choosing the format
^^^^^^^^^^^^^^^^^^^

If you have a database table with Molfiles, we recommend that you use:

-  Molfiles if you are too busy to convert anything and not so
   interested in performance. Performance will be acceptable anyway.
-  SMILES if you are interested in performance but do not undertake 3D
   searches and do not use the highlighting feature frequently.
-  Internal binary format if you are interested in performance and need
   3D searches or use the highlighting feature often.
-  GZip-compressed Molfiles if you are interested in performance but not
   allowed to use any format other that Molfile. Normally, you would not
   need that option.

If you have a database table with Rxnfiles, the recommendations are the
same, but please note that the reaction SMILES format does not contain
the reacting centers information. So if you need the reacting centers in
the database reactions, use Rxnfiles or binary format. If you do not use
the highlighting frequently, you can choose not to save atom positions.

Choosing the Oracle Data Type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For molecule and reaction storage, Bingo supports the following Oracle
data types equally well:

-  Character Large Object (CLOB)
-  Binary Large Object (BLOB)
-  String (VARCHAR2), limited to 4000 characters by Oracle

We recommend that you use:

-  CLOB for Molfiles and Rxnfiles
-  VARCHAR2 for SMILES and reaction SMILES
-  BLOB for binary format or GZip-compressed data

However, you can use any data type for any of the supported formats.
Please consider the limitation of VARCHAR2 to 4000 characters. This
number of characters is more than enough for SMILES, but usually it is
not enough for Molfiles and Rxnfiles.

Mixing formats
^^^^^^^^^^^^^^

Mixing different formats in the database is not a problem. For example,
you can insert SMILES string to CLOB column that contains Molfiles.

Conversion
^^^^^^^^^^

You can convert molecules and reactions from any format to any other
format using Bingo operators, namely ``Molfile()``, ``Rxnfile()``,
``SMILES()``, ``RSMILES()``, ``CompactMolecule()``,
``CompactReaction()``, ``Zip()``, and ``Unzip()``. See below for
details.

**Note:** Conversion operators work only for target (database) molecules
and reactions. Query features are not supported for conversion.

Performance Notice
^^^^^^^^^^^^^^^^^^

Oracle stores table data in cached
`blocks <http://download.oracle.com/docs/cd/B28359_01/server.111/b28318/logical.htm#i4894>`__
in a row-wise manner. That means, the more data in each row, the more
blocks that Oracle has to read from disk to fetch one column with
molecule or reaction number. In order to minimize the number of blocks
(and so minimize the query completion time), you may want to include
less data in table rows. This is the reason for using the compact
formats like SMILES or Bingo binary format.

**Note:** If you have both columns with large items (Molfiles/Rxnfiles)
and compact items (SMILES/binary) in one table, the query performance
will be even worse than with the single Molfile/Rxnfile column. The
benefits of compact formats are evident when you separate the compact
table from the initial large one.
