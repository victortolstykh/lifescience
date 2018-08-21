The following command creates the index:

::

    CREATE INDEX $index ON $table ($column) INDEXTYPE IS Bingo.ReactionIndex;

``$table`` is the name of the table containing reaction data in the
column ``$column``. ``$index`` is the unique name of the Oracle domain
index that will be created.
