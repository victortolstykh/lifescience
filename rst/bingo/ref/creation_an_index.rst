The following command creates the index:

::

    CREATE INDEX $index ON $table ($column) INDEXTYPE IS Bingo.MoleculeIndex;

``$table`` is the name of the table containing molecule data in column
``$column``. ``$index`` is the unique name of the Oracle domain index
that will be created.

You can disable the computation of specific fingerprint parts (saving
both time and disk space), setting the corresponding parameter to zero:

-  ``FP_ORD_SIZE=0``, if you are not planning to undertake a
   substructure or SMARTS search often;
-  ``FP_TAU_SIZE=0``, if you are not planning to undertake a tautomer
   substructure search often;
-  ``FP_ANY_SIZE=0``, if your substructure search queries will not
   contain a lot of query features;
-  ``FP_SIM_SIZE=0``, if you will never use similarity search
   capability.

Here is an example to turn off “any” and “tautomer” fingerprint bits:

::

    CREATE INDEX $index on $table($column) INDEXTYPE IS Bingo.MoleculeIndex PARAMETERS('FP_TAU_SIZE=0 FP_ANY_SIZE=0');

Without fingerprints, you will still be able to perform the search, but
it will run slowly. In order to make it run fast, you will need to
re-create the index with the fingerprints enabled.

You can specify number of parallel threads for the index creation
procedure. For example, if you want to use only one core of your
multi-core CPU, please set the number of threads to one:

::

    CREATE INDEX $index on $table($column) INDEXTYPE IS Bingo.MoleculeIndex PARAMETERS('NTHREADS=1');

The default value for ``NTHREADS`` is zero, which means that the number
of threads will be equal to the number of CPU cores (auto-detected) plus
one.
