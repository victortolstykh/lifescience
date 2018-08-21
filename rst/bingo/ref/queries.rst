You can specify the query molecule as a Molfile (including various query
features), or as a SMILES string. For reaction queries, use Rxnfiles or
reaction SMILES. As for Oracle data types, CLOB and VARCHAR2 are
supported for queries.

**Note:** In order to make substructure and SMARTS search faster, Bingo
loads the indexed molecules into memory. The loading itself takes some
time, and as a result, the first substructure or SMARTS query runs
slower than all the subsequent ones. The loaded molecules are shared
across other SQL sessions, and so other sessions there will not
encounter such time lags. The memory is freed as soon as all the
sessions working with this table are disconnected.
