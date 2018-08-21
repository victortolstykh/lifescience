The ``Bingo.InChI`` operator can be used to generate
`InChI <http://www.inchi-trust.org/inchi/>`__ string for a given
molecule structure. The operator has two arguments: molecule and
options, and returns CLOB result.

::

    SELECT Bingo.InChI($molecule, $options) FROM DUAL;

    SELECT Bingo.InChI($binary, $options) FROM DUAL;

    SELECT Bingo.InChI($column, $options) FROM $table;

You can pass any options supported by the official InChI library. This
options can be found in the InChI manual or on the `InChI FAQ
page <http://www.inchi-trust.org/technical-faq>`__.
Usage example:

::

    SELECT Bingo.InChI('CC1CC(C)OC(C)N1', '') FROM DUAL;

    SELECT Bingo.InChI('CC1CC(C)OC(C)N1', '/DoNotAddH /SUU /SLUUD') FROM DUAL;

    SELECT Bingo.InChI('CC1CC(C)OC(C)N1', '-DoNotAddH -SUU -SLUUD') FROM DUAL;

Each option can start with ``\`` or ``-`` symbol.

The ``Bingo.InChIKey`` operator can be used to generate
`InChIKey <http://www.inchi-trust.org/fileadmin/user_upload/html/inchifaq/inchi-faq.html#2.7>`__
from InChI string:

::

    SELECT Bingo.InChIKey('InChI=1S/C6H6O/c7-6-4-2-1-3-5-6/h1-5,7H') FROM DUAL;

    SELECT Bingo.InChIKey(Bingo.InChI('OC1=CC=CC=C1', '')) FROM DUAL