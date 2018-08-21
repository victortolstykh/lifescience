The ``Bingo.RSMILES()`` operator can be used for converting Rxnfiles and
binary reactions to reaction SMILES. The operator works equally well
with CLOB, BLOB, and VARCHAR2 operands. The operator always returns the
VARCHAR2 result.

::

    SELECT Bingo.RSMILES($rxnfile) FROM DUAL;

    SELECT Bingo.RSMILES($binary) FROM DUAL;

    SELECT Bingo.RSMILES($column) FROM $table;

**Note:** If the input reaction is badly formed (i.e. does not accord to
any format, has drawing mistakes or has unsupported features), Bingo
throws the exception to Oracle.

Converting a Table
^^^^^^^^^^^^^^^^^^

When you convert a table to reaction SMILES, you have two possibilities
for skipping the bad exception- raising reactions:

**1.** Short option:

::

    CREATE TABLE $newtable AS SELECT $id $newid, Bingo.RSMILES($rxnfile) $rsmiles FROM $table
                                             WHERE Bingo.CheckReaction($rxnfile) IS NULL;

**2.** Lengthy but faster option:

::

    CREATE TABLE $newtable ($newid NUMBER, $rsmiles VARCHAR2(4000));

    set serveroutput on;
    declare
      i int := 0;
    begin
      dbms_output.enable(1000000);
      for item in (select $id, $rxnfile from $table) loop
        begin
          INSERT INTO $newtable values(item.$id, bingo.RSMILES(item.$rxnfile, 1));
        exception
          when others then 
            dbms_output.put_line('Bad reaction '|| item.$id ||': ' || SQLERRM);;
        end;
        i := i + 1;
        if i mod 1000 = 0 then
          COMMIT;
        end if;
      end loop;
    end;

``$table`` contains Rxnfiles in the ``$rxnfile`` column and the reaction
ID-s in the ``$id`` column. ``$newtable`` will contain reaction SMILES
in the ``$rsmiles`` column and reaction ID-s in the ``$newid`` column.
