## Unterschied Translation vs. Interpretation
L0 bis LX: Abstraktionsschichten von Code

Translation:    abstrakter Code (L1) wird zeilenweise in Code in Schicht darunter (L0) übersetzt und ausgeführt

Interpretation: Programm in L0 nimmt abstrakten Code (L1) als Eingabedaten und führt Befehle zeilenweise in L0-Code aus

Bei Translation entsteht Intermediärprogramm in L0, das ausgeführt wird. Das L1-Programm wird verworfen. Bei der Interpretation entsteht *kein* solches Intermediärprogramm und der Code wird direkt ausgeführt.

## Begriffe

Compiler:   Ein Programm, welches Code in höherer Sprache (L5) in Assembly (L4) oder system calls (L3) übersetzt. Bsp.: Java Byte Code in JVM

Register:   Gruppierung von mehreren Logikgattern zur Speicherung von Daten als Arbeitsspeicher.

Cache:  kleiner, schneller Arbeitsspeicher, welcher nahe der CPU existiert und häufig verwendete Daten zwecks schneller Verfügbarkeit speichert. D.h. je größer und schneler der Cache ist, desto schneller kann die CPU arbeiten.

Linker: Programm, welches Prozeduren in Quellcode im Hauptspeicher (RAM) lädt. Es verbindet (linkt) einzelne Prozeduren (Module) in ein Objektmodul. Die einzelnen Prozeduren werden einzeln vom Compiler und Assembler translatiert und in derselben Schicht gelinkt.
Bsp.:
UNIX    p1.o
        p2.o    -->-- Linker --> ausführbare Binärdatei
        p3.o

Windows p1.obj
        p2.obj  -->-- Linker --> p.exe
        p3.obj

statisches Linken:  Objektmodule werden vor Programmausführung gelinkt.

## Speichereinheiten
1 MB    =   1x10^6 B    =   1048576 B
1 MiB   =   1x2^20 B    =   1000000 B

Geschwindigkeiten sind in Bits, **nicht** in Bytes pro Zeiteinheit angegeben!
D.h. diese sind langsamer, als man auf den ersten Blick denken könnte.
1 KB ist *eigentlich* 1000 B, wird aber wie KiB (2^10 B = 1024 B) behandelt.
