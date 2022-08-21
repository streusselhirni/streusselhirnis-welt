---
title: 'TrueNAS - Teil 1: Hardware'
date: 2022-08-20T20:34:00+02:00
draft: true
cover:
  image: header.jpeg
  caption: Photo by [Patrick Lindenberg](https://unsplash.com/@heapdump?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/harddrive?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
---
TrueNAS ist ein Betriebssystem mit dem man seinen Computer in eine NAS verwandeln kann. Mit der passenden Hardware lässt sich so eine leistungsfähige, auf die eigenen Bedürfnisse zugeschnittene NAS selbst bauen. Welche Vorteile das bringt und worauf man achten muss, erzähle ich in dieser Serie, die meine Reise von Recherche über Zusammenbau und Einrichtung bis zur Inbetriebnahme erzählt.
<!--more-->

Manchmal bin ich schon ein bisschen ein "Sammler", Zumindest im digitalen Bereich. Zwar bin ich noch lange nicht so schlimm, wie die Kollegen drüber bei [/r/DataHoarding](https://reddit.com/r/DataHoarding), dennoch habe ich in den letzten Jahren eine beachtliche Film- und Musiksammlung aufgebaut. Zusammen mit Fotos und weiteren Daten hat sich einiges an Daten angesammelt.
Bis anhin waren diese Daten auf einer QNAP-NAS mit zwei 4TB Festplatten gespeichert. 

Einfache Consumer-NAS-Systeme von Synology und QNAP leiden heutzutage an denselben Update-Obdoleszenz-Problemen wie moderne Smartphones: Irgendwann sagen die Hersteller "Dieses System ist zu alt, es gibt keine Updates mehr" und dann gibt die NAS langsam immer wie mehr die Funktion auf. Dies war nun auch bei bei QNAP der Fall. Zusätzlich fiel sie in letzter Zeit mit Fehler auf, so sind zum Beispiel manche Dateien nicht mehr auffindbar und das System hängt regelmäßig fest.

Durch einige Videos von [Linus Tech Tips](https://www.youtube.com/channel/UCXuqSBlHAE6Xw-yeJA0Tunw) wurde ich an das Betriebssystem [TrueNAS](https://www.truenas.com/) erinnert. Dabei handelt es sich um ein NAS-Betriebssystem, welches man auf seiner Hardware installieren kann. So ist es ganz einfach möglich, sich seine "eigene NAS" zu bauen: Man besorge sich die passende Hardware, installiere das Betriebssystem und viola: eine NAS Marke Eigenbau!

## Was ist TrueNAS?

[TrueNAS](https://www.truenas.com) ist ein auf FreeBSD basierendes Betriebssystem zum Betrieb von [Network Attached Storage (NAS)](https://de.wikipedia.org/wiki/Network_Attached_Storage). TrueNAS verwendet standardmäßig das [ZFS Dateisystem](https://de.wikipedia.org/wiki/ZFS_(Dateisystem)) und unterstützt damit alle Vorteile, die dieses mit sich bringt: Deduplizierung, Kompression, Snapshots, Copy-on-write, Redundanz, sehr gute Performance und mehr. TrueNAS existiert bereits seit mehr als zehn Jahren und ist entsprechend "erwachsen" und stabil.

Alternativen für solche NAS-Betriebssysteme sind [OpenMediaVault](https://www.openmediavault.org/) und [Unraid](https://unraid.net/de). Beide können theoretisch auch ZFS nutzen, jedoch ist die ZFS-Unterstützung bei keinem von beiden so zentral eingebaut wie bei TrueNAS. Unraid ist zudem nicht kostenlos. So ist meiner Meinung nach TrueNAS die beste Option. Unraid ist zwar auch ein sehr gutes Produkt, aber der Fakt, dass es nicht kostenlos ist und ZFS nur begrenzt unterstützt bringt mich wieder zurück zu TrueNAS.

## Vorgehen

Ist die Entscheidung, sich eine eigene NAS auf Basis von TrueNAS zuzulegen gefallen, geht es erst mal an die Planung. Der erste Schritt – abgesehen von der Entscheidung natürlich – ist die Hardware. Hier hat man grundsätzlich zwei Möglichkeiten:

1. Einen fertigen Server kaufen: Natürlich kann man einfach einen vorgefertigten Speicher-Server kaufen. Es gibt aber auch den Hersteller [iXSystems](https://www.ixsystems.com/), der fertige Hardware, die speziell für TrueNAS zertifiziert ist, anbietet. Leider sind diese in Europa aber nur schwer zu bekommen und zweitens sind sie relativ teuer: Das Einsteigermodell TrueNAS Mini E fängt bei 849 USD an und hat noch keine Festplatten enthalten.

{{<figure src="truenas-mini-e.jpg" caption="Screenshot aus dem iXSystems-Amazon-Shop" >}}

2. Einzelne Komponenten kaufen und selber bauen: Eine TrueNAS ist nur ein Server und ein Server ist auch nur ein Computer. Folglich kann man sich auch genau auf die eigenen Bedürfnisse zugeschnittene Hardware aussuchen, organisieren und selbst zusammen bauen. Dabei muss man nur darauf achten, dass die gewählte Hardware mit TrueNAS kompatibel ist. Dies ist jedoch meistens kein großes Problem, da TrueNAS auf FreeBSD (oder Debian im Falle von TrueNAS SCALE, dazu später mehr) basiert, wird die meiste Hardware problemlos unterstützt. Dies ist die Route, die ich wählte.

## Exkurs: TrueNAS CORE vs. TrueNAS SCALE vs. TrueNAS Enterprise
Wie ich feststellen musste, hat TrueNAS mittlerweile zwei Produkte in petto: CORE und SCALE. CORE ist die altbekannte TrueNAS-Distribution, die auf FreeBSD basiert und in den letzten zehn Jahren stabil gealtert ist. SCALE ist ein neueres Produkt, welches wohl erst vor kurzem aus dem Beta-Status herauskam. Es basiert auf Debian Linux und hat Unterstützung für KVM-Virtualisierung und Kubernetes. Enterprise ist dann die - wer hätte es gedacht - Enterprise-Lösung für Firmen. Sie basiert grundsätzlich auf CORE, ist aber nicht kostenfrei erhältlich. Ein ausführlicher Vergleich der drei Editionen gibt es [hier](https://www.truenas.com/compare-editions/).

Da Enterprise Geld kostet, habe ich dieses sofort ausgeschlossen. Allerdings schwankte ich etwas zwischen CORE und SCALE. Insbesondere die Virtualisierungs-Möglichkeiten von SCALE haben es mir sehr angetan. Da ich aber bereits einen separaten Proxmox-basierten Virtualisierungs-Server zuhause habe (den ich auch bald ersetzen möchte), entschied ich mich, auf Stabilität zu setzen und CORE zu verwenden.

## Hardware-Anforderungen

Zunächst galt es zu klären, welche Anforderungen ich an die NAS und damit an die Hardware habe. Außerdem musste sichergestellt werden, dass die Hardware-Anforderungen von TrueNAS gut erfüllt werden, denn an einer schlecht performenden NAS hätte ich am Ende keinen Spaß. Erste Anlaufstelle für diese Informationen ist die offizielen Dokumentation von TrueNAS, wo es einen [Hardware Guide](https://www.truenas.com/docs/core/gettingstarted/corehardwareguide/) gibt. 

### Prozessor

Die Anforderungen an die CPU sind relativ gering. TrueNAS verlangt nur eine 64-bit CPU auf Basis der x86-Architektur mit zwei Kernen. Damit können eigentlich fast alle Prozessoren von Intel oder AMD verwendet werden. 

Die Frage war also, wieviel Leistung ist brauchte. Da das System ja als NAS quasi durchgehend, Tag und Nacht, laufen soll, war für mich noch ein weiterer Punkt von Bedeutung: Wieviel Strom verbraucht der Prozessor? Ich recherchierte also ein bisschen auf der Suche nach einem Prozessor, der möglichst wenig Strom verbraucht und trotzdem relativ gute Leistung bietet. Diese Recherche sah in ungefähr so aus: Auf verschiedenen Vergleichsseiten und Shop suchte ich nach Prozessoren, die mindestens vier Kerne hatten und sortierte das Ergebnis danach nach TDP (Thermal Design Power: Für welche Leistungsaufnahme der Prozessor konzipiert ist). Zusätzlich versuchte ich einige Google-Suchen im Stile von "low tdp cpu for home server" und las mich etwas durch einige Foren- und Reddit-Threads.

So fand ich schlussendlich zum [Intel Core i3-8100T](https://www.intel.de/content/www/de/de/products/sku/129944/intel-core-i38100t-processor-6m-cache-3-10-ghz/specifications.html), ein auf dem LGA1151-Sockel aufbauender Prozessor von 2018 mit vier Kernen, vier Threads 3.1Ghz Grundtakt und nur 35 Watt Verlustleistung, den es zum Zeitpunkt des Schreibens dieses Posts ab rund [136€](https://geizhals.de/intel-core-i3-8100t-cm8068403377415-a1795934.html) zu kaufen gibt. Natürlich gäbe es auch neuere Alternativen. Intels i3-Platform hat grundsätzlich das beste Verhältnis von Leistung zu Stromverbrauch. Die neuen Core i3 der 11. und 12. Generation wären mit 35-45 Watt TDP genauso gut geeignet. Die Prozessoren sind auch nicht viel teurer als der von mir gewählte i3-8100T, da allerdings der Sockel ebenfalls neuer ist, wären das dazu passende Mainboard dann ganz schnell auch teurer geworden.

Um etwas Geld zu sparen, habe ich dann noch einen Blick auf eBay geworfen. Dort fand ich ein Angebot für einen Intel Core i3-8100 (man bemerke das fehlende T) inklusive dem Intel-Stock-Kühler und einer Tube Wärmeleitpaste. Die letzten beiden Dinge müsste ich, falls ich den i3-8100T neu kaufen würde noch separat dazu kaufen, was sich auf rund 100-150€ Mehrkosten gegenüber dem eBay-Angebot belaufen würde. Der i3-8100 hat zwar eine Verlustleistung von 65W (statt der 35W der 8100T), sollte aber im Idle-Modus, in dem er sich ja die meiste Zeit befindet, deutlich weniger verbrauchen. Mit Blick darauf, dass ich vielleicht doch mal Plex oder einen anderen Serverdienst zusätzlich auf der TrueNAS laufen lassen möchte, ist die Zusatzleistung der 8100 gegenüber des 8100T auch nicht verschenkt.

{{<figure src="i3-8100.jpeg">}}

### Mainboard

Die Auswahl des Mainboards war etwas einfacher als des Prozessors. Von TrueNAS gibt es hier keine besonderen Vorgaben, wichtig ist nur, dass es die benötigten Anschluss in der gewünschten Geschwindigkeit hat und dass der Prozessor-Sockel stimmt. Mein Vorgehen war, auf [PCPartPicker](https://pcpartpicker.com) zu gehen und dort einfach nach Mainboards zu filter, die vom Sockel her passen und mindestens vier SATA-Anschlüsse für Festplatten haben. Dann habe ich nach [Preis sortiert](https://de.pcpartpicker.com/products/motherboard/#s=30&K=4,13&sort=price&page=1). So fand ich das **ASRock H310CM-DVS**, ein günstiges Motherboard für rund 46€, welches meinen Prozessor unterstützt, vier SATA3-Anschlüsse hat und sonst tatsächlich nicht viel. Keine ECC-RAM-Unterstützung (diese hätte mir zuviel gekostet), nur zwei RAM-Steckplätze (was aber reicht) und leider auch nur 1Gbit/s-Netzwerk. Die zwei größten Mankos (1Gbit/s-Netzwerk und nur vier SATA-Anschlüsse) lassen sich aber mit PCIe-Erweiterungskarten ausbessern. Zwar hat das Mainboard auch hier nur einen PCIe x1- und einen PCIe x16-Anschluss, aber das reicht schon. Dafür war es günstig.

{{<figure src="asrock-h310cm-dvs.jpeg">}}

### Arbeitsspeicher

Nun zum Arbeitsspeicher. TrueNAS benötigt mindestens 8GB, damit das Betriebssystem überhaupt läuft. Da TrueNAS jedoch auf dem [ZFS Dateisystem](https://de.wikipedia.org/wiki/ZFS_(Dateisystem)) aufbaut, profitiert es ungemein von mehr Arbeitsspeicher. Insbesondere Funktionen wie z. B. Deduplizierung und Kompression benötigen Unmengen von Arbeitsspeicher. TrueNAS empfielt zusätzlich zu den 8GB Mindestanforderungen noch mindestens weiteres 1GB für jede angeschlossene Festplatte und weiterer RAM abhängig davon, welche Funktionen, Dienste oder Container noch ausgeführt werden soll. Nach [TrueNAS' Liste](https://www.truenas.com/docs/core/gettingstarted/corehardwareguide/#memory-sizing) bräuchte ich, mit meinen geplanten vier Festplatten also "nur" 12 bis 17GB RAM, je nachdem ob ich Deduplizierung nutzen möchte und wieviele Daten dedupliziert werden sollen.

Da Arbeitsspeicher in Zweierpotenzen verkauft wird und mir 16GB zu knapp bemessen waren, habe ich mich für 32GB entschieden. Um etwas an Performance herauszuholen, sollte der Arbeitsspeicher im Dual Channel-Modus laufen. Das bedeutet, dass ich nicht nur einen 32GB-Stick einbauen sollte, sondern zwei 16GB-Stick. So arbeitet der Speicher effizienter. Ich habe dann einfach wieder auf [PCPartPicker](https://pcpartpicker.com) nach einem RAM-Packet mit 2x16GB gesucht und dabei darauf geachtet, dass es das zum Mainboard passende Format (DDR4-2133, DDR4-2400 oder DDR-2666) ist. So wurde es der Corsair Vengeance LPX 32 GB.

{{<figure src="corsair-vengeance.jpeg">}}

### Gehäuse

Fehlt nur noch das Gehäuse. Hier gilt es eigenlich nur darauf zu achten, dass alle Komponenten rein passen. Ich habe ursprünglich nach NAS-Gehäusen gesucht, die einen HDD-Käfig haben oder evt. hot-swappable Festplatten unterstützen, jedoch waren alle Gehäuse, die ich fand, entweder zu teuer oder die von mir gewählten Komponenten haben dort nicht reingepasst. Falls jemand anderes solche Gehäuse sucht: Der Hersteller [SilverStone Tek](https://www.silverstonetek.com/de/product/computer-chassis/?page=1&filter=Server_chassis&sort=Newsest) scheint einige gute im Angebot zu haben.

Nachdem ich etwas recherchiert hatte ("NAS-Gehäuse" und ähnliches bei Google gesucht), stieß ich in einem Forum auf das [Cooler Master Silencio S400](https://www.coolermaster.com/catalog/cases/mini-tower/silencio-s400/). Die Schalldämmung ist ein schönes Feature, es hat Platz für alles und war mit 93€ preislich im Rahmen. Also wurde es das.

{{<figure src="case.jpeg">}}

### Netzteil

Das ganze System benötigt ja auch noch Strom, als müssen wir noch ein Netzteil suchen. Da ich die gesamte Konfiguration bis hierher auf PCPartPicker zusammengestellt hatte, konnte ich auch gleich das Netzteil dort suchen. PCPartPicker unterstützt einen dabei schön, denn es zeigt die ungefähr benötigte Leistung direkt an. So wusste ich, dass ich mindestens 390 Watt einplanen sollte.

Wichtig bei Netzteilen ist, dass man keine Experimente wagt. Da schlechte oder defekte Netzteile wirklich gefährlich werden können (Explosions- und Brandgefahr!), lohnt es sich, bei der Wahl des Netzteiles auf bekannte Marken und Hersteller wie SeaSonic oder Corsair zu setzen. Natürlich muss der Formfaktur ins Gehäuse passen. Wie beim Prozessor schon, wollte ich bei meiner NAS etwas auf den Stromverbrauch achten, weswegen ich mich entschied, beim Netzteil auf ein Effizients-Rating von mindestens 80+ Platinum setzen wollte (höheres Effizienz-Rating spart Strom). So wurde es das SeaSonic Focus 550.

### Speicher

Last but for sure not least: Speicherplatz! Was wäre eine NAS ohne Speicherplatz? Auch hier gibt es Seitens TrueNAS kaum Vorgaben. Solange die Speichermedien mit dem Rest des Systems kompatibel sind, sollte TrueNAS es ebenfalls unterstützen.

Klassischweise wird eine NAS mit Festplatten betrieben und aus Kostengründen entschied ich mich, auch weiterhin auf klassische Festplatten zu setzen, denn diese bieten immer noch das beste Verhältnis zwischen Speicherplatz und Preis. Wie auch schon beim Netzteil, lohnt es sich bei Festplatten auf bekannte Hersteller zu setzen. Die beiden größten sind Western Digital (WD) und Seagate. Beide Hersteller haben verschiedene Lineups von Festplatten, davon ist mindestens eine für den Dauerbetrieb in Speichersystemen geeignet. Bei WD ist es das Red-Lineup bei Seagate ist es IronWolf. Kapazitäts-technisch habe ich bereits auf vier 4TB-Platten festgelegt, dies ist meiner Meinung nach ein guter Mittelweg zwischen "noch für mich bezahlbar" und "möglichst viel Speicher".

Schlussendlich wurden es vier Platten der WD Red 4TB Serie, einfach weil diese 10€ günstiger waren als das Gegenstück von Seagate. Nichtsdestotrotz haben die vier Festplatten gleich viel gekostet, wie der ganze Rest des Systems zusammen.

Neben den Festplatten, die der NAS zur Verfügung stehen sollen, benötigt TrueNAS noch ein Boot-Laufwerk, als ein weiteres Laufwerk, auf welchem das Betriebssystem installiert wird. Dies kann theoretisch auch ein USB-Stick sein, wobei TrueNAS davon abrät. Ich hatte zuhause noch eine PCIe-SATA-Erweiterungskarte und eine ältere Intel-SSD herumliegen. Mit der PCIe-Karte kann ich das System um vier weitere SATA-Anschlüsse erweitern (und habe damit insgesamt 8 SATA-Anschlüsse zur Verfügung), die SSD nutze ich als Boot-Laufwerk.

### Zusammenfassung

Somit komme ich insgesamt auf die folgende Hardware:

| Komponente  | Produkt                                                                    | Preis   | Händler          |
|-------------|----------------------------------------------------------------------------|---------|------------------|
| CPU         | Intel Core i3-8100 3.6 GHz Quad-Core Processor                             | 75,94€  | eBay             | 
| Motherboard | ASRock H310CM-DVS Micro ATX LGA1151 Motherboard                            | 34,89€  | Mindfactory      |
| Memory      | Corsair Vengeance LPX 32 GB (2 x 16 GB) DDR4-2400 CL14 Memory              | 101,90€ | Amazon           |
| Storage     | 4x Western Digital Red 4 TB 3.5" 5400RPM Internal Hard Drive               | 376€    | Mindfactory      |
| Case        | Cooler Master Silencio S400 MicroATX Mini Tower Case                       | 88,90€  | ComputerUniverse |
| Power Supply| SeaSonic FOCUS 550 W 80+ Platinum Certified Fully Modular ATX Power Supply | 89,29€  | Amazon           |
| PCIe-Sata-Erweiterungskarte | unbekannt, hatte ich noch rumliegen                        | 0€      |                  |
| Kabel      | 5 SATA3-Kabel                                                               | 4,50€   | Amazon           |
| **Total**  |                                                                             | **766,92€** |              |

Die Hardware ist nun bestellt, jetzt heißt es abwarten. Im nächsten Post dokumentiere ich dann den Zusammenbau und die Einrichtung von TrueNAS. Seid gespannt!