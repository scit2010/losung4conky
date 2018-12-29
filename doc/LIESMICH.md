# Beschreibung
*Losungen für Conky* ist ein kleines Programm, das die täglichen Losungstexte der Herrnhuter Brüdergemeine in Conky anzeigt.
Aus technischer Sicht ist es ein Perl-Skript, dessen Ausgabe im Conky-Fenster angezeigt wird. 

# Copyright
## Losungen
(C) Evangelische Brüder-Unität - Herrnhuter Brüdergemeine: www.herrnhuter.de
Weitere Informationen: www.losungen.de

## Losungen für Conky
(C) Sven Claussner
Das Programm (aber nicht die Losungstexte) ist unter der GPL, Version 3 oder später, lizenziert, s. Datei COPYING.

# Voraussetzungen
Das Programm benötigt Linux, einen Perl-Interpreter und den Systemmonitor Conky. Außer zum erstmaligen Download des Programms und des Systemmonitors Conky und gegebenenfalls der Losungstexte ist keine Internetverbindung erforderlich.
Eine aktuelle Fassung der Losungstexte ist im Programmarchiv enthalten. 
Das Programm wurde erfolgreich mit Perl 5, Conky 1.7-1.10 und verschiedenen Linux-Distributionen und Desktopumgebungen getestet.

# Anleitung
## Installation
1. Entpacken Sie die Archivdatei in ein temporäres Verzeichnis.
2. Installieren Sie als Benutzer 'root' mit dem Befehl 'make install' das Programm.
   Standardmäßig wird das Programm dabei in das Verzeichnis /usr/local/bin installiert.
   Sie können ein anderes Verzeichnis angeben, indem sie den Befehl 
   'make DEST=<Zielverzeichnis> install' (ohne die spitzen Klammern) aufrufen.
3. Passen Sie ihre Datei .conkyrc an: 
   1. Tragen Sie im Konfigurationsabschnitt (vor der Zeile TEXT) ein:
      text_buffer_size 768
   2. Tragen Sie im Inhaltsabschnitt (nach der Zeile TEXT) an der gewünschten
      Position den Aufruf des Programms losung.pl ein. Hinweise und Kopiervorlagen 
      zur Konfiguration der Datei .conkyrc finden Sie in der Datei conkyrc-1.9-example (für Conky 1.9) oder conkyrc-1.10-example (für Conky 1.10). 
4. Starten Sie Conky unter ihrer normalen Benutzerkennung. Falls Conky schon gestartet war, als Sie Schritt 3 ausführten, sollten die Änderungen nach Ablauf des Aktualisierungsintervalls (in der Regel wenige Sekunden) wirksam werden. Andernfalls beenden Sie Conky und starten es erneut.

## Deinstallation
1. Führen Sie als Benutzer 'root' den Befehl 'make uninstall' aus oder löschen Sie die Dateien losung.pl und losungen*.csv im Programmverzeichnis manuell.
2. Machen Sie die Änderungen in der Datei .conkyrc (s.Schritt 3  der Installationsanleitung) rückgängig.
3. Starten Sie Conky. Falls Conky schon gestartet war, als Sie Schritt 2 ausführten, sollten die Änderungen nach Ablauf des Aktualisierungsintervalls (in der Regel wenige Sekunden) wirksam werden. Andernfalls beenden Sie Conky und starten es erneut.

# Fehler und Lösungen
Im Folgenden bezeichnet das Kürzel <Jahr> das jeweils aktuelle Jahr, z.B. 2011.
Fehlerbehebungen werden abhängig von den Einstellungen für das Aktualisierungsintervall (Konfigurationseintrag update_interval in der Datei .conkyrc) zeitverzögert wirksam.


## Anstelle der Losungen erscheint gar nichts.
### Ursachen
1. Möglicherweise haben Sie die Installation nicht richtig durchgeführt.
2. Die Einstellungen in der Konfigurationsdatei .conkyrc sind für den verwendeten Fenstermanager bzw. die verwendete Desktopumgebung (GNOME, KDE usw.) ungeeignet.

### Lösung
Zu 1.:
Wiederholen Sie die Installation. Falls Sie das Programm in ein anderes als das standardmäßige Programmverzeichnis installiert haben, tragen Sie dieses Verzeichnis auch in den Aufruf in der Datei .conkyrc ein. Vorlagen dafür finden Sie in den Dateien conkyrc-1.9-example (für Conky 1.9) und conkyrc-1.10-example (für Conky 1.10). 

Zu 2.:
Öffnen Sie in Ihrem Home-Verzeichnis die Datei .conkyrc. 
Stellen Sie fest, welche Desktopumgebung Sie benutzen.
Entfernen Sie für Ihre Desktopumgebung die Kommentarzeichen "# " bzw. "-- " vor den Einstellungen.
Speichern Sie die Datei.


## Anstelle der Losungen erscheint der Fehlertext "The file losungen<Jahr>.csv is missing."
### Ursache
Das Programm kann die Losungsdatei "losungen<Jahr>.csv" nicht finden. 
### Lösung
Diese Datei befindet sich in der Archivdatei. Kopieren Sie die Datei von dort in das Programverzeichnis, in dem sich das Programm losungen.pl befindet.


## Anstelle der Losungen wird der Fehlertext "You don't have read permissions for file losungen<Jahr>.csv." angezeigt.
### Ursache
Sie verfügen nicht über Leseberechtigungen für die Losungsdatei "losungen<Jahr>.csv". 
### Lösung
Verändern Sie oder Ihr Administrator die Zugriffsberechtigungen für diese Datei, sodass Sie als Benutzer die Leseberechtigung für diese Datei haben (Befehl 'chmod +r losungen<jahr>.csv')


## Anstelle der Losungen erscheint der Fehlertext "The file losungen<Jahr>.csv is corrupted."
### Ursache
Die Losungsdatei liegt in einem ungültigen Format vor.
### Lösung
Ersetzen Sie die Losungsdatei im Programmverzeichnis durch eine gültige Fassung aus der Archivdatei.


## Der angezeigte Losungstext enthält anstelle von Umlauten unleserliche Symbole.
### Ursache
Die Losungsdatei ist beschädigt. 
### Lösung
Ersetzen Sie die Losungsdatei im Programmverzeichnis durch das Original aus dem Programmarchiv. 


## Unter KDE 4 erscheinen die Losungen doppelt und überlagert. Sie sind dadurch unleserlich.
### Ursache
Conky wurde zweimal oder öfter gestartet. Zum Beispiel könnte er beim Anmelden automatisch gestartet sein und wurde zusätzlich durch die Autostart-Mechanismen 
in KDE erneut gestartet.
### Lösung
1. Öffnen Sie ein Terminalfenster (Programm "Konsole").
2. Führen Sie den Befehl ps -ef | grep conky aus. 
3. Von allen Zeilen, die in der letzten Spalte nur den Eintrag 'conky' enthalten, notieren Sie sich den Wert in der zweiten Spalte (das ist die Prozessnummer).
4. Führen Sie den Befehl kill -9 $Prozessnummer aus (ersetzen Sie dabei $Prozessnummer durch den Wert aus Schritt 3). Wiederholen Sie diesen Schritt bis nur noch ein einzelner Conky-Prozess läuft.
5. Falls sich in ihrem HOME-Verzeichnis in der Datei .profilerc die Zeile 'conky &' befindet, entfernen Sie diese und speichern die Datei.
