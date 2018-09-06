User Manual: Oracle
===================

Basics
------

Data representation
~~~~~~~~~~~~~~~~~~~

.. include:: ref/data_representation.rst


Storage
~~~~~~~

.. include:: ref/storage.rst


Indices
~~~~~~~

.. include:: ref/indices.rst


Queries
~~~~~~~

.. include:: ref/queries.rst


Molecules
---------

Conversion to SMILES
~~~~~~~~~~~~~~~~~~~~

.. include:: ref/conversion_to_SMILES.rst


Creating an Index
~~~~~~~~~~~~~~~~~

.. include:: ref/creation_an_index.rst


Substructure Search
~~~~~~~~~~~~~~~~~~~

.. include:: ref/substructure_search.rst


SMARTS Search
~~~~~~~~~~~~~

.. include:: ref/smarts_search.rst


Exact Search
~~~~~~~~~~~~

.. include:: ref/exact_search.rst


Tautomer Search
~~~~~~~~~~~~~~~

.. include:: ref/tautomer_search.rst


Similarity Search
~~~~~~~~~~~~~~~~~

.. include:: ref/similarity_search.rst


Gross Formula Search
~~~~~~~~~~~~~~~~~~~~

.. include:: ref/gross_formula_search.rst


Molecular Mass Search
~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/molecular_mass_search.rst


Canonical SMILES
~~~~~~~~~~~~~~~~

.. include:: ref/canonical_SMILES.rst


Molecule Fingerprints
~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/molecule_fingerprints.rst


InChI and InChIKey
~~~~~~~~~~~~~~~~~~

.. include:: ref/InChI_and_InChIKey.rst



Reactions
---------

Conversion to Reaction SMILES
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/conversion_to_reaction_SMILES.rst


Conversion to binary format
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/conversion_to_binary_format.rst


Creating an Index
~~~~~~~~~~~~~~~~~

.. include:: ref/reaction_creation_an_index.rst


Exact Search
~~~~~~~~~~~~

.. include:: ref/reaction_exact_search.rst



SMARTS Search
~~~~~~~~~~~~~

.. include:: ref/reaction_SMARTS_search.rst


Substructure Search
~~~~~~~~~~~~~~~~~~~

.. include:: ref/reaction_substructure_search.rst


Automatic Atom-to-Atom Mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/automatic_atom-to-atom_mapping.rst



Reaction Fingerprints
~~~~~~~~~~~~~~~~~~~~~

.. include:: ref/reaction_fingerprints.rst


Nonstandard Queries
-------------------

Finding Non-Matches
~~~~~~~~~~~~~~~~~~~

You can specify zero right side in the Bingo operator calls in order to
find targets that do *not* match the query.

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query, $parameters)=0;

    SELECT * FROM $table WHERE Bingo.Exact($column, $query, $parameters)=0;

    SELECT * FROM $table WHERE Bingo.Gross($column, $query, $parameters)=0;

    SELECT * FROM $table WHERE Bingo.RSub($column, $query)=0;

Fragment Highlighting
~~~~~~~~~~~~~~~~~~~~~

Along with the results of the substructure search, you can get back the
target molecules or reactions in Molfile/Rxnfile v3000 format with the
query fragment highlighted.

::

    SELECT $id, Bingo.SubHi(1) FROM $table WHERE Bingo.Sub($column, $query, 1)=1;

You can also do an affine transformation or a conformation search in
this manner.

::

    SELECT $id, Bingo.SubHi(1) FROM $table WHERE Bingo.Sub($column, $query, 'AFF $rms', 1)=1;

    SELECT $id, Bingo.SubHi(1) FROM $table WHERE Bingo.Sub($column, $query, 'CONF $rms', 1)=1;

SMARTS search results also can be viewed with highlighting:

::

    SELECT $id, Bingo.SmartsHi(1) FROM $table WHERE Bingo.SMARTS($column, $query, 1)=1;

When performing tautomer search, you can highlight the tautomeric chains
that differ in query and target.

::

    SELECT $id, Bingo.ExactHi(1) FROM $table WHERE Bingo.Exact($column, $query, 'TAU $parameters', 1)=1;

In tautomer substructure search, both the fragment and chains are
highlighted.

::

    SELECT $id, Bingo.SubHi(1) FROM $table WHERE Bingo.Sub($column, $query, 'TAU $parameters', 1)=1;

For reaction substructure search, you can highlight the query reaction
in the target reaction.

::

    SELECT $id, Bingo.RSubHi(1) FROM $table WHERE Bingo.RSub($column, $query, 1)=1;

Examples of highlighting are all over the User Manual. The highlighted
fragments in the examples are rendered in bold font and double bond
width.

**Note:** In case the matched molecule or reaction does not have layout
information (i.e. is represented as SMILES or binary format with atom
positions switched off), the automatic layout procedure is performed.

You can also convert the highlighted Molfiles/Rxnfiles to SMILES, which
will contain the highlighting information encoded to a format
understandable by `Indigo <../indigo/index.html>`__ toolkit, and
particularly by the `indigo-depict <../indigo/indigo-depict.html>`__
utility:

::

    SELECT $id, Bingo.SMILES(Bingo.SubHi(1)) FROM $table WHERE Bingo.Sub($column, $query, 1)=1;

    SELECT $id, Bingo.SMILES(Bingo.SmartsHi(1)) FROM $table WHERE Bingo.SMARTS($column, $query, 1)=1;

Multiple Conditions and Joins
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can mix the cartridge operators with other (standard) operators to
restrict the set of fetched results:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query)=1 AND $molweight < $value;

Mixing various Bingo operators is also possible:

::

    SELECT * FROM $table WHERE Bingo.Sub($column, $query)=1 AND Bingo.Gross($column, '>= C20')=1;

You can select from two or more tables:

::

    SELECT * FROM $table1, $table2 WHERE
         Bingo.Sub($column1, $query1)=1 AND Bingo.Sub($column2, $query2)=1 AND
         Bingo.Gross($column1)=Bingo.Gross($column2);

**Note:** In case ``$query`` is a VARCHAR2 string, Bingo is able to make
use of Oracle's Cost-Based Optimizer (CBO) capability. This capability
allows Oracle to call single operator functions rather than to use the
index implementation, if the former gives higher performance
expectations.

**Note:** A CLOB ``$query`` does not take advantage of CBO due to the
technical limitation of Oracle.

Importing and Exporting Data
----------------------------

Importing SDFiles, RDFiles, and SMILES files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can import a molecule or reaction table from an SDF file. You can
also import SDF fields corresponding to each record in the SDF file.
Prior to importing, you have to create the table manually and grant to
``Bingo`` the access to insert to your table:

::

    CREATE TABLE $table(..., $column CLOB, ...);
    GRANT INSERT ON $table to Bingo;
    EXEC Bingo.ImportSDF('$table', '$column', '$other_columns', '$filename');

-  ``$table`` is the name of the table subject to import, *including the
   schema qualifier*.
-  ``$column`` is the name of the CLOB column containing the data in
   Molfile or Rxnfile format.
-  ``$other_columns`` is the comma-separated list of space-separated
   'property-column' pairs that are to be imported. Each given SDF
   property is mapped to the given table column. You can specify an
   empty string or NULL if there are no properties to import.
-  ``$filename`` is the location of the resulting file on the *server
   filesystem*.

One can import a part of PubChem database (stored, for example, in
``pubchem.sdf`` file) with the following commands:

::

    CREATE TABLE STRUCTURES(cid INT, structure CLOB, name VARCHAR2(4000), mw NUMBER);
    GRANT INSERT ON STRUCTURES to Bingo;
    EXEC Bingo.ImportSDF('PUBCHEM.STRUCTURES', 'structure',
           'pubchem_compound_cid cid, pubchem_iupac_name name, pubchem_molecular_weight mw',
           '/tmp/pubchem.sdf');

GZip-compressed data is detected automatically in ``ImportSDF``, and so
you can call it the same way:

::

    EXEC Bingo.ImportSDF('PUBCHEM.STRUCTURES', 'structure',
           'pubchem_compound_cid cid, pubchem_iupac_name name, pubchem_molecular_weight mw',
           '/tmp/pubchem.sdf.gz');

Importing RDF files is done with ``ImportRDF()`` function the same way
as SDF files:

::

    CREATE TABLE $table(..., $column CLOB, ...);
    GRANT INSERT ON $table to Bingo;
    EXEC Bingo.ImportRDF('$table', '$column', '$other_columns', '$filename');

Importing multi-line molecule or reaction SMILES file is done the
similar way with the ``ImportSMILES()`` function:

::

    CREATE TABLE $table($id INT, $column VARCHAR2(4000));
    GRANT INSERT ON $table to Bingo;
    EXEC Bingo.ImportSMILES('$table', '$column', '$id', '$filename');

-  ``$table``, ``$column``, and ``$filename`` have the usual meaning
-  ``$id`` is the column where molecule and reaction identifiers go. The
   identifier within SMILES string is anything that goes after the
   molecule or reaction, separated by space. It is allowed to pass an
   empty string or NULL as the ``$id`` parameter, if there are no
   identifiers in the SMILES file subject to import.

**Note:** When you import the file contents to a table, the old table
contents are not removed. Thus, you can import multiple files into the
same table.

**Note:** You cannot use these procedures without granting to ``Bingo``
the access to select from/insert to your table.

Exporting SDFiles
~~~~~~~~~~~~~~~~~

Exporting SDF files is conducted in a similar way to importing, except
that you have to grant to ``Bingo`` the access to select from your table
rather than insert to it: You can export the molecule or reaction table
to an SDF file.

::

    EXEC Bingo.ExportSDF($table, $column, $other_columns, $filename);

Example of exporting the PubChem database to the ``/tmp/pubchem.sdf``
file:

::

    EXEC Bingo.ExportSDF('PUBCHEM.COMPOUNDS', 'structure', 'cid name mw', '/tmp/pubchem.sdf');

You can also export the table to a GZip-compressed SDF file:

::

    EXEC Bingo.ExportSDFZip($table, $column, $other_columns, $filename);

In this case, please do not forget to append ``.gz`` to the file name:

::

    EXEC Bingo.ExportSDFZip('PUBCHEM.COMPOUNDS', 'structure', 'cid name mw', '/tmp/pubchem.sdf.gz');

Utility Functions
-----------------

Extracting the Names of Molecules and Reactions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``Bingo.Name`` function extracts the molecule or reaction name from
Molfile, Rxnfile, or SMILES string.

::

    SELECT bingo.Name(molfile) from mytable;

    SELECT bingo.Name('c1ccc2ccccc2c1 Naphthalene') from DUAL;

Conversion to Molfiles/Rxnfiles and CML
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the ``Bingo.Molfile`` operator to convert SMILES or binary molecule
back to Molfile:

::

    SELECT Bingo.Molfile($smiles) from DUAL;

    SELECT Bingo.Molfile($binary) from DUAL;

    SELECT Bingo.Molfile($column) from $table;

Use the ``Bingo.Rxnfile`` operator to convert reaction SMILES or binary
reaction back to Rxnfile:

::

    SELECT Bingo.Rxnfile($rsmiles) from DUAL;

    SELECT Bingo.Rxnfile($binary) from DUAL;

    SELECT Bingo.Rxnfile($column) from $table;

Use the ``Bingo.CML`` operator to convert SMILES or Molfile to the [CML]
(http://en.wikipedia.org/wiki/Chemical\_Markup\_Language) format:

::

    SELECT Bingo.CML($smiles) from DUAL;

    SELECT Bingo.CML($binary) from DUAL;

    SELECT Bingo.CML($column) from $table;

Similarly, the ``Bingo.RCML`` operator returns the input reaction
converted to the CML format:

::

    SELECT Bingo.RCML($smiles) from DUAL;

    SELECT Bingo.RCML($binary) from DUAL;

    SELECT Bingo.RCML($column) from $table;

**Note**: If the input molecule of reaction is badly formed (i.e. does
not conform to any format, has drawing mistakes or has unsupported
features), Bingo throws the exception to Oracle.

**Note**: In case the input molecule or reaction does not have layout
information (i.e. is represented in reaction SMILES or binary format
with atom positions switched off), the automatic layout procedure is
performed.

Checking Molecules and Reactions for Correctness
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use the ``Bingo.CheckMolecule()`` function to check that
molecules are presented in acceptable form:

::

    SELECT Bingo.CheckMolecule($molecule) from DUAL;
    SELECT Bingo.CheckMolecule($column) from $table;

If the molecule is correct, the function returns NULL. Otherwise, it
returns the VARCHAR2 string with the error message. For example, you can
select all incorrect molfiles from the table by the following query:

::

    SELECT * from (SELECT $id, Bingo.CheckMolecule($molfile) cm FROM $table) WHERE cm is not null;

You can check reactions for correctness with the
``Bingo.CheckReaction()`` function:

::

    SELECT Bingo.CheckReaction($reaction) from DUAL;
    SELECT Bingo.CheckReaction($column) from $table;
    SELECT * from (SELECT $id, Bingo.CheckReaction($rxnfile) cr FROM $table) WHERE cr is not null;

Reading and Writing Files on Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The ``Bingo.FileToClob()`` function accepts a VARCHAR2 file path and
loads a file from the server file system to Oracle CLOB.

::

    SELECT Bingo.FileToClob($path) FROM DUAL;

Usually you may want to load the query molecule in the following way:

::

    SELECT * form $table WHERE Bingo.Sub($column, Bingo.FileToClob($path))=1;

The ``Bingo.ClobToFile()`` procedure accepts a CLOB and VARCHAR2 file
path and saves the CLOB to the server file system.

::

    EXECUTE BEGIN Bingo.ClobToFile($lob, $path); END;

GZip Compression and Decompression
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can use ``Bingo.Zip()`` function to convert CLOBs to BLOBs which are
in fact GZip data:

::

    CREATE TABLE $gztable as SELECT $id, Bingo.Zip($data) $gzdata FROM $table;

Table indexing and all queries should work on compressed Molfile/Rxnfile
BLOB-s exactly the same way as they work on ordinary Molfile/Rxnfile
CLOB-s. To uncompress the data back, please use Bingo.Unzip() function:

::

    SELECT Bingo.Unzip($gzdata) FROM $gztable;

**Note:** Normally, you would not need these functions, as long as you
have a possibility of using SMILES and Bingo compact formats for
molecules and reactions.

Maintenance
-----------

Obtaining the Bingo Version Number
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can get the product version from the following query:

::

    select Bingo.GetVersion from DUAL;

Viewing the Log File
~~~~~~~~~~~~~~~~~~~~

The log file is called ``bingo.log`` and located in the system temporary
directory on the server file system. Usually it is:

-  ``/tmp/bingo.log`` on Linux and Solaris
-  ``C:\Windows\Temp\bingo.log``, ``C:\WINNT\Temp\bingo.log``, or
   ``C:\TEMP\bingo.log`` on Windows

All operation of Bingo is logged. All error and warning messages (not
necessarily visible in SQL session) are logged. Most importantly, the
Oracle ROWID of each indexed molecule or reaction is recorded, and so
you could easily find the molecules and/or reactions that have caused
problems. Some performance measures of the SQL queries are written to
the log as well.

.. include:: ref/images.rst

