The ``Bingo.CompactReaction()`` operator can be used for converting
Rxnfiles and reaction SMILES to internal binary format. The operator
works equally well with CLOB, BLOB, and VARCHAR2 operands. The operator
always returns the BLOB result.

::

    SELECT Bingo.CompactReaction($rxnfile, $xyz) FROM DUAL;

    SELECT Bingo.CompactReaction($rsmiles, $xyz) FROM DUAL;

    SELECT Bingo.CompactReaction($column, $xyz) FROM $table;

The ``$xyz`` parameter must be 0 or 1. If it is 1, the positions of
atoms are saved to the binary format. If it is zero, the positions are
skipped.

**Note:** If the input reaction is badly formed (i.e. does not conform
to any format, has drawing mistakes or has unsupported features), Bingo
throws the exception to Oracle.

Converting a table
^^^^^^^^^^^^^^^^^^

When you convert a table to binary format, you have two possibilities
for skipping the bad exception-raising reactions:

**1.** Short option:

::

    CREATE TABLE $newtable AS SELECT $id $newid, Bingo.CompactReaction($rxnfile, &xyz) $binary FROM $table
                                      WHERE Bingo.CheckReaction($rxnfile) IS NULL;

**2.** Lengthy but faster option:

::

    CREATE TABLE $newtable ($newid NUMBER, $binary BLOB) lob($binary) store as (enable storage in row);
    set serveroutput on;

    declare
      i int := 0;
    begin
      dbms_output.enable(1000000);
      for item in (select $id, $rxnfile from $table) loop
        begin
          INSERT INTO $newtable values(item.$id, bingo.CompactReaction(item.$rxnfile, $xyz));
        exception
          when others then 
            dbms_output.put_line('Bad reaction '|| item.$id ||': ' || SQLERRM);
        end;
        i := i + 1;
        if i mod 1000 = 0 then
          COMMIT;
        end if;
      end loop;
    end;
