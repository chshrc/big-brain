Ein "state" ist eine fixe Reihenfolge an Bits (bspw. in Hauptspeicher, Prozessen oder Kernel)("Zustand").

Die Hauptaufgaben des Linux-Kernels sind folgende Systembereiche:
Prozesse, Hauptspeicher, Gerätetreiber, Systemaufrufe und Support

In jedem Zeitabschnitt ("time slice"), sei es Sekunde, Millisekunde usw., kann nur *ein* Prozess in der CPU aufgerufen werden.
Der Wechsel zwischen Prozessen in der CPU heißt Kontextwechsel ("context switch"). Die Fähigkeit, mehrere Prozesse scheinbar gleichzeitig laufen zu lassen, heißt "multitasking".

Die MMU ("memory management unit") hilft der CPU bei der Speicherverwaltung im Hauptspeicher. Sie stellt Prozessen Speicheradressen in einer "page table" zur Verfügung, die beim context switch vom Kernel in reale Adressen im Hauptspeicher ausgetauscht werden ("virtual memory").

Systemaufrufe ("syscalls") sind Aufrufe des Kernels durch Anwederprozesse ("user processes"), die user processes helfen, bestimmte Aufgaben zu erfüllen, die diese entweder schlecht oder nicht ausführen können/dürfen.
Bsp.: fork() und exec()

fork()  erstellt eine nahezu identische Kopie eines Prozesses
exec()  wird mit einem Programm als Argument aufgerufen, welches den aufrufenden Prozess ersetzt

In Linux werden *alle* (Ausnahme init()) Prozesse mittels fork() gestartet oder mittels exec() ersetzt. Bsp.: Befehl `ls` in Shell:
shell mit PID 5 ruft fork() auf; der neue Prozess mit der PID 6 ruft exec(ls) auf

Der Bereich für user processes, den der Kernel im Hauptspeicher reserviert, heißt "user space" oder "userland". Innerhalb des user space können user processes in Ebenen unterteilt werden.
Diese unterscheiden sich in der "Nähe" zum Anwender bzw. dem Kernel auf sich gegenüberliegenden Seiten.

Der superuser "root" läuft, wie alle user processes, im user mode und *nicht* im kernel mode.
