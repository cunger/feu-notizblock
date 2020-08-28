# Pascal Cheatsheet

## Bezeichner (Identifier)

```pas
letter [letter, digit]*
```

Stil-Regeln:

* Konstanten gross (`PI`, `MAX`, `MIN`)
* Variablen in Camel Case (`greatestCommonDivisor`)
* Typenvariablen mit t beginnen (`tIndex`, `tColor`)

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

  procedure p(inVar : real, outVar : boolean);
  { Beschreibung, was die Prozedur macht. }

    var
    ...

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
  days  : array [ integer ] of tWeekday;      { Array, Index kann integer, boolean, char sein }
  map   : array [ tColor ] of integer;        { Arrays können wie Maps verwendet werden }
  m     : array [ integer, integer ] of real; { Multi-dimensionales Array, z.B. für Matrizen }

begin
 ...
end.
```

## Strings

Länge: `length(str)`

Auf die Zeichen in einem String kann über Indizes von 1 bis `length(str)` zugegriffen werden (d.h. `str[1]` bis `str[length(str)]`). Strings sind _mutable_, d.h. einzelne Zeichen können ersetzt werden (z.B. `str[1] := 'c'`).

## Arrays


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