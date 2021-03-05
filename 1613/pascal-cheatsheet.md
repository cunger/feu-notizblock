# Pascal Cheatsheet

## Bezeichner (Identifier)

```pas
letter [letter, digit]*
```

Stil-Regeln:

* Konstanten gross (`PI`, `MAX`, `MIN`)
* Variablen in Camel Case (`greatestCommonDivisor`)
* Typenvariablen mit `t` beginnen (`tIndex`, `tColor`)

## Programmstruktur

```pas
program ProgrammStruktur;
{ Beschreibung, was das Programm macht. }

  const
  ...

  type
  ...

  var
  ...

  function f(num : real) : boolean;
  { Beschreibung, was die Funktion macht. }

    var
    ...

  begin
    ...
    f := true { Der Ausgabewert der Funktion wird dem Funktionsparameter zugewiesen. }
  end;

  procedure p(inA : integer, var ioB, outC : integer);
  { var-Parameter: Referenzübergabe (call-by-reference)
    andere Parameter: Wertübergabe (call-by-value) }

    var
    ...

    { Der Skopus von Variablen in Blockstrukturen ist lexikalisch,
      also der bei Definition, nicht bei Aufruf. }

  begin
    ...

    { Prozeduren haben keine Ausgabewert. Sie können auch nicht als Teile von Ausdrücken
      verwendet werden, nur als eigenständige Anweisung. }
  end;

begin
  ...
end.
```

## Typen

```pas
program Typen;
{ Überblick über primitive und abgeleitete Typen. }

  type
  tColorRange = 0..250;
  tOpacity = 0.0..1.0;
  tWeekday = (Mon, Tue, Wed, Thu, Fri, Sat, Sun); { Enum }
  tColor = record
             R,
             G,
             B : tColorRange;
             opacity: tOpacity;
           end;

  var
  i1,
  i2    : integer;
  num   : real;
  b     : boolean;                            { Werte: true, false }
  c     : char;
  str   : string;                             { z.B. 'Fnord' }
  color : tColor;
  days  : array [ 1..7 ] of tWeekday;         { Array, der Indextyp kann integer, boolean, char
                                                und Enums und Ranges sein; Stil-Regel:
                                                implizite Typendefinitionen wie hier vermeiden }
  map   : array [ tColor ] of integer;        { Arrays können also wie Maps verwendet werden }
  m     : array [ integer, integer ] of real; { Multi-dimensionales Array, z.B. für Matrizen }

begin
 ...
end.
```

## Strings

Länge: `length(str)`

Auf die Zeichen in einem String kann über Indizes von 1 bis `length(str)` zugegriffen werden (d.h. `str[1]` bis `str[length(str)]`). Strings sind _mutable_, d.h. einzelne Zeichen können ersetzt werden (z.B. `str[1] := 'c'`).

## Arrays

```pas
type
tRow = 1..9;
tCol = 1..9;

tVector = array [tCol] of integer;
tMatrix = array [tRow, tCol] of integer;

var
vector = tVector;
matrix = tMatrix;

begin
  { Zuweisung }

  vector[1] := 0;
  vector[2] := 0;
  ...

  matrix[1, 1] := 4;
  matrix[1, 2] := 7;
  ...

  { Zugriff }

  writeln(vector[1] * matrix[1, 1] + vector[2] * matrix[1, 2]);
end.
```

## Schleifen

```pas
while <condition> do
  <statement> ;

repeat
  <statement>
until <condition> ;

for i := 1 to 10 do
  <statement> ;

for i := 10 downto 1 do
  <statement> ;

n := 10;
for i := 1 to n do { call-by-value }
begin
  n := n - 1;      { d.h. Änderungen an n haben keinen Effekt auf die Schleife }
  i := 0           { Error: illegal assignment to for-loop variable "i" }
end;
```

## Zeiger

```pas
type
tList = array [ 0..9 ] of integer;
tRefList = ^tList; { Zeigertyp }
tLinkedList = record
                value : integer;
                next  : tRefList
              end;

var
refAnchor = tRefList;    { Zeigervariable, Anfang der Linked List }
refFirst  = tLinkedList;
refSecond = tLinkedList;

begin
  refAnchor := nil; { Initialisierung der Zeigervariable als leeren Zeiger. }

  new(refFirst); { Erzeugt ein neues Objekt vom Type tLinkedList und }
                 { weist refFirst einen Zeiger auf dieses Objekt zu. }  

  { Der Zeiger verweist auf die Speicheradresse dieses Objekts. }

  { Dereferenzierung: refFirst^ hat das Objekt als Wert }
  { und kann also wie jedes Objekt von dem Typen verwendet werden. }

  refFirst^.wert := 1;
  refFirst^.next := refAnchor;

  new(refSecond);
  refSecond^.wert := 2;
  refSecond^.next := refFirst;

  { Vergleich: ref1 = ref2 , wenn ref1^ = ref2^ }
  { Zwei Zeiger sind also gleich, wenn die Objekte, auf die sie zeigen, }
  { entweder beide nil oder wertgleich sind (d.h. sie müssen nicht das  }
  { gleiche Objekt im Speicher sein). }

  dispose(refFirst);  { Zeigervariable zeigt jetzt wieder ins Leere. }
  dispose(refSecond);
end.  
```
