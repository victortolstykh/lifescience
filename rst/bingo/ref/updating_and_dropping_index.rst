You can add, remove, or edit records in the table after the index is
created. Adding records does not slow down the queries, i.e. the
performance will be the same as if you had indexed the whole table at
once. No re- indexing is required after adding the records.

You can drop the index at any time. After the drop, the queries will
slow down but return the same results.

**Note:** Due to technical limitations with Oracle, adding the molecules
in an indexed table is slower than indexing the existing molecules. For
example, if you have an indexed table with 5000 molecules and if you
want to add another 50000, dropping the index before adding and
re-creating it would be a good decision. On the other hand, if you have
50000 indexed molecules, adding another 5000 will be faster if you do
not re-index.

**Note:** If you delete or replace substantial amount of records in the
indexed table, re-creating the index in order will speed up the queries.

After you insert or update, you must either:

-  close the SQL session, or
-  execute ``Bingo.FlushInserts()`` procedure.

to make the inserted/updated rows available for other SQL sessions. If
there are no other sessions that are using the table you are updating,
this is not necessary.

**Note:** You must call ``FlushInserts()`` before doing ``INSERT`` or
``UPDATE`` of the same table from another session. If you do another
``INSERT`` or ``UPDATE`` concurrently from another session, it will hang
until the first session does ``FlushInserts()`` or terminates.

``FlushInserts()`` takes some time, and as a result, it is not included
in the ``INSERT`` and ``UPDATE`` implementations. You do not need to
call ``FlushInserts()`` after each ``INSERT`` or ``UPDATE``. It is
normal to call it after you have finished updating the table.

Here is an example:

::

    CREATE INDEX $index ON $table ($column) INDEXTYPE IS Bingo.MoleculeIndex;
    INSERT INTO $table (SELECT * FROM $other_table);
    EXECUTE BEGIN Bingo.FlushInserts(); END;
