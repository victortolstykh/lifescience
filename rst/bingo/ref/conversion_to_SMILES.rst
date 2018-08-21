The ``Bingo.SMILES()`` operator can be used for converting Molfiles and
binary molecules to SMILES. The operator works equally well with CLOB,
BLOB, and VARCHAR2 operands. The operator always returns the VARCHAR2
result.

::

    SELECT Bingo.SMILES($molfile) FROM DUAL;

    SELECT Bingo.SMILES($binary) FROM DUAL;

    SELECT Bingo.SMILES($column) FROM $table;

**Note:** If the input molecule is badly formed (i.e. does not conform
to format, has drawing mistakes, or has unsupported features), Bingo
throws the exception to Oracle.

Converting a Table
^^^^^^^^^^^^^^^^^^

When you convert a table to SMILES, you have two possibilities for
skipping the bad exception-raising molecules:

**1.** Short option:

::

    CREATE TABLE $newtable AS SELECT $id $newid, Bingo.SMILES($molfile) $smiles FROM $table
                                           WHERE Bingo.CheckMolecule($molfile) IS NULL;

**2.** Lengthy but faster option:

::

    CREATE TABLE $newtable ($newid NUMBER, $smiles VARCHAR2(4000));

    set serveroutput on;
    declare
      i int := 0;
    begin
      dbms_output.enable(1000000);
      for item in (select $id, $molfile from $table) loop
        begin
          INSERT INTO $newtable values(item.$id, bingo.SMILES(item.$molfile));
        exception
          when others then 
            dbms_output.put_line('Bad molecule '|| item.$id ||': ' || SQLERRM);
        end;
        i := i + 1;
        if i mod 1000 = 0 then
          COMMIT;
        end if;
      end loop;
    end;

``$table`` contains Molfiles in the ``$molfile`` column and molecule IDs
in the ``$id`` column. ``$newtable`` contains SMILES in the ``$smiles``
column and molecule IDs in the ``$newid`` column.
