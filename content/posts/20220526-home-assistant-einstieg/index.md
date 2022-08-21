---
title: "Home Assistant: Ein Einstieg"
date: 2022-05-26T21:49:17+02:00
draft: false
cover:
    image: header.jpeg
    caption: Photo by [Ihor Saveliev](https://unsplash.com/@saveli?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) / [Unsplash](https://unsplash.com/?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit)
---

Wer sein Zuhause schlau machen will, hat einige Möglichkeiten: Apple Home, Google Nest, Amazon Alexa, u.v.m. Alle haben sie gemeinsam, dass man wahrscheinlich seine Seele an eine amerikanische Firma verkaufen muss.

Doch es gibt auch andere Lösungen. An dieser Stelle möchte ich euch [Home Assistant](https://www.home-assistant.io/) vorstellen. Home Assistant ist eine Software, mit deren Hilfe verschiedenste Smart Home- und IoT-Geräte gesteuert und automatisiert werden können. Der Clou: Das ganze wird lokal im eigenen Netzwerk gehostet, man ist also nicht auf "die Cloud" angewiesen und sendet keine Daten an irgendwelche Firmen in Übersee.

{{<figure src="home-assistant-logo.svg" caption="Logo des Home Assistant">}}

Bevor ich darauf eingehe, wie Home Assistant eingerichtet werden kann (Spoiler: Irgendeine Form von Server wird benötigt, dies kann aber auch eine neuere NAS oder ein Raspberry Pi sein), möchte ich kurz erzählen, was man alles damit machen kann.

Über sogenannte Integrationen können eine beinahe unendliche Menge von Geräten mit Home Assistant verbunden werden: Neben den "Klassikern" wie Philip Hue, Nanoleaf, Nuki, Eve, Trådfri, SmartThings, Zigbee oder Z-Wave, gibt es auch Integrationen für eher außergewöhnliche Geräte wie Home Connect, Denon, Deutsch Bahn, Fritzboxen, sogar Abfahrtszeiten für schwedische Fähren können eingebunden werden.

{{<figure src="screenshot1.png" caption="Integrations-Seite von Home Assistant">}}

Nachdem man einige Geräte hinzugefügt hat, geht der Spaß erst richtig los: Nun können wir Dashboards, Automationen und Szenen erstellen und die Geräte in Areale und Zone einteilen.

## Dashboards

Mit Home Assistant kannst du beliebig viele Dashboards erstellen. Ein Dashboard ist eine (Internet-)Seite, für die du völlig beliebig entscheiden kannst, welche Informationen angezeigt werden sollen. Zur Verfügung stehen "Informationspanels", aber auch Knöpfe zum Ein-/Ausschalten von Lichtschaltern, Grafiken für Luftbefeuchter u.ä., Bildflächen zur Verschönerung und vieles mehr.

{{<figure src="screenshot2.png" caption="Ein einfaches Dashboard">}}

Diese Dashboards können zum Beispiel auf einem an der Wand montierten Tablet angezeigt werden. Oder in einen selbstgebauten Smart-Spiegel integriert werden. Oder, oder, oder. Ich selbst muss zugeben, dass ich das Dashboard bisher nicht großartig nutze...

## Das Kerngeschäft: Automationen

Der Grund, warum die meisten – eigentlich wohl alle – Home Assistant installieren, wird aber wohl die Automation sein. Eine HA-Automation besteht aus drei Teilen:

**Trigger** – Für jede Automation können ein oder mehrere Auslöser definiert werden. Diese Auslöser können quasi alles sein: Der Batteriestand eines Handys, ein Anruf, das Signal eines Bewegungsmelders. So ziemlich jedes Gerät, dass in HA integriert werden kann und einen "Zustand" hat, der sich ändern kann, kann als Auslöser verwendet werden.

**Bedingungen** – Eine Automation soll unter Umständen nicht uneingeschränkt dauernd ausgeführt werden; dafür sind Bedingungen gut. Ein Beispiel: Ich habe einen Bewegungsmelder im Flur, der das Licht einschaltet. Allerdings soll er dies nur tagsüber und nur, wenn es nicht sowieso hell genug ist, machen. Neben dem Trigger (Bewegung), gibt es also zwei Bedingungen: Zeit und Helligkeit. Nur wenn beide erfüllt sind (oder auf Wunsch auch nur eine der beiden), werden die Aktionen ausgeführt.

**Aktionen** – Der dritte und letzte Punkt ist natürlich der wichtigste: Die Aktionen. Wir wollen ja, das etwas passiert. Auch hier kann so ziemlich alles angesteuert werden, was etwas tun kann: Schlaue Glühbirnen, Switchbots, Zigbee- oder Z-Wave-Geräte, Smart-Bewässerungsgeräte, Kameras, u.v.m.

## Vor- und Nachteile

Man mag sich jetzt nun fragen: "Warum sollte ich denn Home Assistant einrichten?". Abschließend erzähle ich noch ein bisschen von den Vorteilen von Home Assistant.

* Self-Hosted: Home Assistant läuft vollständig bei dir Zuhause. Keine Cloud-Anbindung nötig, kein Senden von Daten an irgendwelche amerikanischen Firmen!
* Flexibel: Mit Home Assistant sind der Fantasie keine Grenzen gesetzt. Dank der riesigen Menge von Integrationen kann so ziemlich jedes Gerät und jeder Sensor in deine Routinen eingebunden werden.
* Optionen: Es gibt so gut wie nichts, was nicht mit Home Assistant möglich ist. Ziemlich jedes Smart-Home-Gerät kann eingebunden und angesteuert werden.

Leider gibt es auch einige Nachteile:

* Komplexität: Die Einrichtung und das Management von Home Assistant benötigt Zeit und etwas Einarbeitung.
* Nicht "set it and forget it": Home Assistant und seine Integrationen werden regelmäßig aktualisiert, doch leider sind (zumindest, wenn man dem Internet glauben darf) immer mal wieder Updates dabei, die etwas kaputt machen. Dann ist manuelle Korrekturarbeit vonnöten.

Ich selbst habe Home Assistant aktuell eingerichtet, verwende es aber nur für einige wenige Automationen. Die meisten meiner Routinen laufen immer noch in Apple Homekit oder direkt über die Philips Hue-Bridge. Da diese Lösungen bisher problemlos laufen, gab es für mich bisher keinen Grund, alles zu Home Assistant zu migrieren (und ich sehe auch keinen Vorteil darin).

Home Assistant nutze ich in erster Linie für diejenigen Automationen, die ich nicht mit Homekit verbinden konnte. Zum Beispiel schickt Home Assistant eine Benachrichtigung auf mein Handy, wenn ein Anruf auf dem Festnetz ankommt. Zusammengefasst: Homekit, wo möglich, Home Assistant als Ergänzung. Bisher läuft das ganz gut!