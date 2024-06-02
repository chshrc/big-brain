## Anwendungsfall
Problem:    Hardware funktioniert nicht korrekt.
Lösung:     Oftmals liegt ein Problem bei der Erkennung der Hardware auf Betriebssystemebene vor. Mit den folgenden Befehlen kann man Hardware auf Linux inspizieren:
            `lspci`:    zeigt mit dem PCI Bus verbundene Geräte an
            `lsusb`:    zeigt mit dem USB Bus verbundene Geräte an

Eine Anzeige von Geräten in der Ausgabe der obrigen Befehle garantiert keine Funktionalität!
Diese wird durch Software bereitgestellt, die die Hardware kontrolliert. Diese Software ist ein sog. Kernel-Modul. Bei Linux-Kernel-Modulen, die mit Hardware in Verbindung stehen, spricht man von Treibern.

## Bootprozess
UEFI/BIOS --lädt--> bootloader --lädt--> Kernel

Der Bootloader kann dem Kernel Bootparameter mitgeben, bspw. für verwendete Rootpartition oder den Modus des Betriebssystems:
`BOOT_IMAGE=/vmlinuz-6.8.0-31-generic root=/dev/mapper/ubuntu--vg-ubuntu--lv ro`

Im ersten Schritt lädt der Kernel die Hardware und konfiguriert diese. Dann wurden die Dienste gestartet, die die übrigen Dienste des Betriebssystems starten.
Ein Beispiel für einen Bootloader ist GRUB.

## Befehle
Wichtige Befehle für diesen Kontext:
* `lspci`
* `lsusb`
* `shutdown`
* `systemctl`
* `journalctl`
* `systemd`

## Partitionierung
Das klassische Schema für die Partitionierung von Laufwerken für Linux ist das MBR-Schema (Master Boot Record).
Die ersten 512 (2^9) Bits beinhalten eine Tabelle, die die Partitionen auf dem Laufwerk beschreiben (Partitionstabelle).

### Festplattenlayout
Speichermedien ("disks") müssen partitioniert werden, um vom Betriebssystem genutzt werden zu können.
Eine Partitionierung ist eine logische Untermenge/Unterteilung eines Speichermediums. Man benötigt mindestens eine Partition pro Speichermedium.
Die Aufteilung in Partitionen wird in einer sog. Partitionstabelle gespeichert.

In jeder Partition existiert ein Dateisystem. Diese beschreibt wie Daten tatsächlich auf dem Medium gespeichert werden.

Partitionen können nicht Bestandteil mehrerer Geräte sein, aber Partitionen auf mehreren Geräten können zu einem einzigen, logischen Volume zusammengefasst werden.

Folgende Partitionen sind günstigerweise getrennt voneinander auf der Festplatte anzulegen:
* `/boot`   --> bei Absturz des Root-Dateisystems ist das System noch bootbar
* `/home`   --> erleichtert Neuinstallation ohne Verlust von Nutzerdaten
* `/var`    --> erleichtert Systemverwaltung, falls mehr Festplattenspeicher für Anwendungen wie Webserver oder Datenbankserver benötigt wird

#### Bootpartition (/boot)
* enthält Dateien für Bootloader; wird üblicherweise in /boot gemounted und die Dateien in /boot/grub gespeichert
* beinhaltet i.d.R. o.a. Dateien, Kernel-Images und RAM-Disk
* gute Größe liegt bei ca. 300 MB

#### ESP (/boot/efi)
* wird für UEFI benötigt, um Bootloader und Kernel-Images für das installierte Betriebssystem zu speichern
* in FAT-Dateisystem formatiert
* auf GUID-partitionierten Festplatten ist die Partition-ID weltweit eindeutig
* auf MBR-partitionierten Festplatten ist die ID "0xEF"

#### Das Homeverzeichnis (/home)
* /home ist nicht zwingend immer der Ort für das Homeverzeichnis der Benutzer (standardmäßig)

#### Variable Daten (/var)
* /var ist ein häufiges Ziel von Prozessen und kann den Speicher komplett ausnutzen
* wenn /var unter / liegt, kann es zu einer Kernelpanic führen

#### Swap-Partition
* dienst als Auslagerung von Speicherseiten des RAM auf das Speichermedium, wenn der RAM nicht ausreicht
* hat bestimmten Partitionstyp
* muss von Programm `mkswap` eingerichtet werden
* Linux unterstützt auch Swap-Dateien statt -Partitionen
Die Größe des RAM ist individuell zu beurteilen.

## LVM
Ein Logical Volume Management (LVM) dient der nachträglichen Verwaltung von Festplattenspeicher.
* in Grundeinheit Physical Volume (PV) unterteilt (kleinste Einheit)
* mehrere PVs werden in Volume Groups (VG) gruppiert; eine VG stellt die Summe des Speichers aller PVs kombiniert dar

1 PE ist i.d.R. ein PV

1 LE besteht aus mehreren PEs

1 LV entspricht der Anzahl aller physischen Einheiten (PE) in MB

Schema:
![Scheme LVM](https://upload.wikimedia.org/wikipedia/commons/b/ba/LVM1.svg)

ein LV wird vom OS als ein Blockgerät betrachtet und in /dev erstellt und als /dev/VGName/LVName bezeichnet

## MBR-Partitionsschema
Der MBR enthält eine Tabelle (Partitionstabelle), die Partitionen auf der Festplatte beschreibt und den als "Bootloader" bezeichneten Bootstrapcode.
Ein Systemstart eines PCs läuft etwa wiefolgt ab:

1. Bootloader wird geladen und ausgeführt
1. Bootloader übergibt Kontrolle an sekundären Bootloader
1. sek. Bootloader lädt das OS

Bsp.: GRUB (steht in MBR)
1. GRUB wird ausgeführt
1. GRUB gibt Kontrolle an ein "Kern"-Iamge (= sek. Bootloader)
1. GRUB lädt zusätzliche Ressourcen von der Festplatte

Weil MBR eine begrenzte Anzahl an Partitionen unterstützt, wurde GPT eingeführt.
GPT ist Teil des UEFI-Standards, aber GPT-partitionierte Festplatten können auch mit PC-BIOS verwendet werden.

Auf BIOS-PCs wird der zweite Teil von GRUB in einer speziellen BIOS-Partition gespeichert.
Auf UEFI-PCs wird GRUB von der Firmware aus den Dateien grubia32.efi oder grubx64.eif von einer Partition names ESP (Efi System Partition) geladen.

Die /boot-Partition enthält für Bootprozess nötige Dateien. Bei allen Dateien steht das Suffix -VERSION für die Version des verwendeten Kernels.
Diese sind Konfigurationsdateien, Systemzuordnung, Linux-Kernel, initiales RAM-Dateisystem, Bootloaderbezogene Dateien.
Der Linux-Kernel ist üblicherweise mit dem Präfix vmlinux- (oder vmlinuz-) versehen.

## Shared Libraries & Shared Objects
Allgemein bezeichnet dies Teile von kompiliertem, wiederverwendbarem Code (z.B. Funktionen oder Klassen), der von verschiedenen Programmen wiederholt verwendet werden kann.

Die Umwandlung von Programm- in ausführbaren Maschinencode geschieht, grob gesagt, in zwei Schritten: Zunächst erstellt der "Compiler" maschinen-ausführbaren Code und speichert diesen in Objektdateien.
Dann verbindet der "Linker" die Objektdateien und "verlinkt" diese mit Bibliotheken, um die endgültig ausführbare Datei zu erstellen.
> In Windows sind diese Bibliotheken mit dem Dateitype `.dll` markiert.

### Statisches und dynamisches Verlinken
Die o.a. Verlinkungen kann statisch oder dynamisch erfolgen.

#### Statisches Verlinken
Wie oben beschrieben "verlinkt" oder "verknüpft" der Linker Bibliotheken mit den Objektdateien zu einem bestimmten Zeitpunkt des Buildprozesses. Nennen wir diesen Zeitpunkt "Verknüpfungszeit".

Beim statischen Verlinken wird die Bibliothek zur Verknüpfungszeit mit dem Programm zusammengeführt. Dabei wird *eine Kopie des Bibliothekscodes in das Programm eingebettet und somit Teil des Programms*. Dadurch hat das Programm *zur Laufzeit* keine Abhängigkeiten zu der Bibliothek, weil es den Bibliothekscode bereits beinhaltet.
Man spricht bei diesen Bibliotheken von "static libraries".

* Vorteil: es ist keine Bereitstellung von Bibliotheken zur Laufzeit des Programms notwendig
* Nachteil: die statisch gelinkten Programme benötigen mehr Speicherplatz

#### Dynamisches Verlinken
Beim dynamischen Verlinken sorgt der Linker dafür, dass das Programm Referenzen zu den benötigten Bibliotheken verwendet.
Es wird hierbei, im Gegensatz zum statische Verlinken, kein Bibliothekscode in das Programm kopiert. Das bedeutet, dass die Bibliothek zur Laufzeit des Programms zur Verfügung stehen muss.
Dieser Ansatz kann als ökonimisch betrachtet werden, da die Programme weniger Speicherplatz benötigen und die sog. "shared libraries" nur einmalig als Kopie in den Speicher geladen werden, selbst wenn diese von mehreren Programmen verwendet wird.

### Namenskonventionen
Eine gemeinsam genutzte Bibliothek ("shared library"; s.o.), also ein "shared object", wird mit einem `soname` betitelt, also einen "shared object name".
Dieser besteht aus den folgenden Teilen:
* Bibliotheksname (meist mit Präfix `lib`)
* `so` (für "shared object")
* Versionsnummer der Bibliothek

Beispiel: `libpthread.so.0`

Bei statischen Bibliotheken enden die Dateien auf `.a`: `libpthread.a`.

In der Praxis ist es gängig, dass man für den Namen der Verlinkung einen allgemeineren Dateinamen verwendet, der wiederum auf die genaue Version der shared library verweist.
Beispiel: `libmlx5-rdmav34.so -> ../libmlx5.so.1.24.50.0`

Übliche Speicherorte für gemeinsam genutzte Bibliotheken unter Linux sind:
* `/lib`
* `/lib32`
* `/lib64`
* `/usr/lib`
* `/usr/local/lib`
