---
title: 'TrueNAS - Teil 2: Installation'
date: 2022-09-04T12:04:04+02:00
draft: true
cover:
  image: header.png
---

Im [letzten Teil]({{< ref "20220820-truenas-hardware" >}} "letzten Teil") habe ich beschrieben, warum ich TrueNAS verwenden möchte und welche Hardware ich dafür verwenden werde. Nun kam die Hardware an! In diesem Beitrag beschreibe ich, wie der Zusammenbau ablief und wie die Installation von TrueNAS funktionert.

<!-- more -->

## Zusammenbau

Zuerst muss Ordnung her. Nachdem die ganze Hardware von vier unterschiedlichen Händlern geliefert war, galt es erstmal zu überprüfen, ob wirklich alles da ist und insbesondere, ob die Verpackungen keine äußerlichen Beschädigungen aufwiesen.

{{<figure src="IMG_0399.jpeg" caption="Die bestellte Hardware">}}

Nun geht es an den Zusammenbau. Für diejenigen, die schon mal einen PC zusammengebaut haben, gibt es hier keine Neuigkeiten. Ich beschreibe hier das grobe Vorgehen in Form einer Fotoserie. Denjenigen, die sich genauer dafür interessieren, wie man einen Computer zusammenbau, empfehle ich etwas Recherche auf YouTube (Linus Tech Tips hat einige gute Videos zum Thema).

{{<figure src="IMG_0407.jpeg" caption="Zuerst wird der Prozessor auf dem Mainboard installiert.">}}

{{<figure src="IMG_0410.jpeg" caption="Auf den Prozessor müssen wir den Kühler platzieren und die RAM-Riegel müssen eingesteckt werden.">}}

{{<figure src="IMG_0413.jpeg" caption="Nun können wir das Mainboard im Gehäuse festschrauben.">}}

{{<figure src="IMG_0416.jpeg" caption="Jetzt das wichtigste: Die Festplatten müssen eingebaut und verkabelt werden.)">}}

{{<figure src="IMG_0419.jpeg" caption="Zum Schlus muss noch alles verkabelt werden. Die letzte Festplatte ist in diesem Gehäuse rechts oben eingebaut und zu sehen. Ebenfalls ist links unten auf dem Mainbaord die zusätzliche PCIe-Sata-Karte zu sehen, die es mir ermöglicht vier weitere Festplatten oder SSDs anzuschließen.">}}

{{<figure src="IMG_0399.jpeg" caption="Zum Abschluss noch das Gehäuse verschließen und fertig ist der Server.">}}

Nachdem nun alles zusammengebaut ist, geht es an die Installation von TrueNAS!

## Installation

Zuerst gilt es, das TrueNAS-Installationsmedium herunterzuladen. Dazu suchen wir auf der TrueNAS-Seite den [Download-Bereich](https://www.truenas.com/download-truenas-core/), wo wir eine Installations-ISO herunterladen können. Mit dieser können wir einen bootfähigen USB-Stick erstellen (z. B. mit dem Programm [Balena Etcher](https://www.balena.io/etcher/)). Dann muss der USB-Stick nur noch in die NAS gesteckt werden und sichergestellt werden, dass wir beim Starten vom USB-Stick booten.

Die Installation von TrueNAS ist dann denkbar einfach. Es gibt einen angenehmen [Installations-Wizard](https://www.truenas.com/docs/core/gettingstarted/install/) dem man grundsätzlich einfach folgen kann. Dieser fragt einen interaktiv zuerst, auf welchem Speichermedium man das Betriebssystem installieren will. Hier habe ich die 120GB SSD, die ich noch herumliegen hatte, ausgewählt. Anschließend wird man gefragt, ob man eine SWAP-Partition erstellen möchte. Diese schadet nicht, ist aber auch nicht unbedingt notwendig, besonders, wenn man 32GB Arbeitsspeicher hat. Zum Abschluss fordert der Wizard einen dazu auf, ein Administrator-Passwort zu setzen. Dann heißt es warten, bis alle Daten installiert wurden.

## Einrichtung

Nach der Installation startet das System neu – an dieser Stelle sollte man auch den Installations-USB-Stick abziehen. Nach dem Neustart zeigt die NAS an, über welche Internet-Adresse (bzw. IP-Adresse) das Web-Interface erreichbar ist. Ab diesem Zeitpunkt kann man theoretisch den Bildschirm von der NAS trennen; alle weiteren Einstellungen werden in der Weboberfläche gemacht.

Loggt man sich in die Weboberfläche ein, wird man von einem Dashboard mit ein paar Hardware-Informationen begrüßt. Nun muss zuerst einmal der Speicherplatz vorbereitet werden. Auch dazu hat TrueNAS eine gute [Dokumentation](https://www.truenas.com/docs/core/gettingstarted/storingdata/). Grundsätzlich muss man nur auswählen, welche Festplatten bzw. Speichermedien für den neuen Speicherpool verwendet werden sollen. Diese werden dann mit dem ZFS-Filesystem im gewünschten RAID-Level initialisiert. Ich habe mich für RAID-Z1 entschieden. Dies ist an sich das gleiche, wie ein Software-RAID-5 von ZFS: Von den vier verwendeten Festplatten wird eine für Paritätsdaten verwendet. Das heißt, dass ich drei Festplatten mit je 4TB Speicher (also total rund 12TB) zur Verfügung habe und zu jeder Zeit maximal eine Festplatte ausfallen könnte. Für weitere Informationen zur Pool-Erstellung sei auf die [TrueNAS-Dokumentation](https://www.truenas.com/docs/core/coretutorials/storage/pools/poolcreate/) verwiesen.

Nach der Erstellung des Speicherpools muss man darauf Datasets erstellen. Datasets sind vergleichbar mit Partitionen von Festplatten, nur sind es rein logische Unterteilungen auf Filesystem-Ebene, die dadurch auch keine feste Größe haben. Hier ist man frei, wieviele Datasets man möchte. Ich habe für jeden geplanten Netzwerk-Share ein Dataset erstellt, denn Einstellungen wie Deduplizerung, Komprimierung oder auch Snapshots werden auf Dataset-Ebene gemacht. Grundsätzlich könnte man aber auch nur ein Dataset haben und einzelne Ordner darin dann als Shares im Netzwerk zur Verfügung stellen.

Damit sind wir auch schon beim letzten – und beinahe wichtigsten – Punkt angelangt: Damit die NAS auch als NAS verwendet werden kann, müssen nun noch sogenannte Shares, zu Deutsch "Netzwerkfreigaben", erstellt werden. Auch dies ist natürlich schön bei [TrueNAS dokumentiert](https://www.truenas.com/docs/core/gettingstarted/sharingstorage/). Damit der Zugriff am Ende auch wie gewünscht funktioniert, müssen zuerst die Zugriffsberechtigungen auf den Datasets richtig gesetzt werden. Ich habe es mir hier relativ einfach gemacht und auf Dataset-Level einfach allen Zugriff auf Alles gegeben. Beim Erstellen des Shares werden dann restriktivere Berechtungen gesetzt. Dies ist für meinen Heimgebrauch ausreichend; in einem Firmenumfeld würde ich von Anfang an restriktiere Berechtigungen setzen.

Vor dem Erstellen der Shares muss man sich noch entscheiden, welche Art von Share man erstellen will. Zur Auswahl stehen Apple Shares (APF), Samba Shares (SMB), Unix Shares (NFS), WebDAV Shares und Block Shares (iSCSI). Die letzten zwei haben sehr konkrete Anwendungsgebiete, auf die ich an dieser Stelle jetzt nicht eingehe. Schlussendlich läuft die Entscheidung für einfache Netzwerkfreigaben darauf heraus, mit welcher Art von Geräten man darauf zugreifen will. Wenn man nur Apple oder Linux-Geräte hat, kann man die entsprechenden APF oder NFS-Shares verwenden. Da aber alle Betriebssysteme Samba können (aber Windows natürlich nicht mit NFS oder APF klarkommt), habe ich mich für SMB-Shares entschieden.

Und schon ist die Einrichtung abgeschlossen. Ein letzter Punkt bleibt aber noch übrig: Irgendwie muss ich die Daten von meiner alten QNAP-NAS auf die neue TrueNAS kopieren. Aber wie?

## Datenmigration

Die Lösung heißt `rsync`. Dabei handelt es sich um ein Kommandozeilenprogramm, welches in der Lage ist, komprimierte und inkrementelle Sicherheitskopien von A nach B zu machen, wobei A und B auch unterschiedliche Geräte sein können. Rsync nutzt dabei eine SSH-Verbindung.

Zuerst muss ich also unter `Services` auf der TrueNAS SSH aktivieren, so dass man von der QNAP auch via SSH auf die TrueNAS verbinden kann. Danach kann man sich per SSH auf die QNAP verbinden. Glücklicherweise war in meinem Fall `rsync` schon installiert, so dass ich nur den passenden Ordner im Dateisystem finden muss und anschließend meine Daten kopieren kann. Ich bin dabei ordner-weise vorgegangen. Als Beispiel konnte ich mit folgendem Befehl meine Film- und Musiksammlung auf die TrueNAS kopieren:

```
rsync -rvzh /share/MD0_DATA/Multimedia root@192.168.178.11:/mnt/box/media
```

Hier werden alle Daten von der QNAP aus dem Ordner `Multimedia` auf die TrueNAS in den Ordner `media` kopiert. `-r` bedeutet rekursiv, so dass auch Unterordner kopiert werden; `-v` ist für "verbose", also dass mehr Informationen ausgeben werden sollen; `-z` steht für "compress", damit die Dateien für die Übertragung komprimiert werden und `-h` zeigt alle Ausgaben in einem "human-readable" Format aus (also z. B. in Gigabyte statt Byte). Der Befehl ist automatisch inkrementell, wenn also was schief lief beim Kopieren, kann er einfach nochmals ausgeführt werden. Rsync merkt dann, welche Dateien bereits kopiert wurden und überspringt diese, so dass nicht alles nochmals kopiert werden muss. Damit der Befehl aber weiterläuft, auch wenn man die SSH-Verbindung schließt, empfielt es sich, den Befehl in einer [Screen-Session](https://www.linux-community.de/ausgaben/linuxuser/2004/09/zu-befehl-screen/) laufen zu lassen.

## Und weiter?

Das Kopieren all meiner Daten hat fast drei Tage gedauert. Danach war aber alles auf der TrueNAS. Und ich merke bereits, dass der Zugriff auf die Daten schneller und stabiler funktioniert. TrueNAS kann aber noch viel mehr. Für die meisten Dienste, die ich Zuhause laufen habe, habe ich einen separaten Server, aber der Prozessor, den ich eingebaut habe, wäre gut in der Lage, auch einige Videos zu transcodieren. Ich plane also, zumindest einen Plex-Server zusätzlich auf TrueNAS laufen zu lassen. Aber das ist ein Thema für einen anderen Blogpost.
