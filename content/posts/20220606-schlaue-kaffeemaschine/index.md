---
title: "Wie eine dumme Kaffeemaschine schlau wurde"
date: 2022-06-06T22:01:55+02:00
draft: false
cover:
    image: header.jpeg
    caption: Photo by [Dylan Calluy](https://unsplash.com/@dylancalluy?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) / [Unsplash](https://unsplash.com/?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit)
---

Wie man eine dumme Kaffeemaschine schlau macht: Dank Switchbots lassen sich Knöpfe via Fernsteuerung und Smart Home-Hubs betätigen. So kann Siri die Kaffeemaschine einschalten!
<!--more-->

Wer kennt es nicht: Da kommt man morgens in die Küche, möchte sich 'nen Kaffee machen und dann muss die Kaffeemaschine erst mal aufheizen. Wie schön wäre es doch, wenn die Kaffemaschine automatisch mit dem Wecker morgens eingeschaltet würde, so dass das morgendliche Gebräu möglichst bald bereit steht.

Genau das war mein Ziel: Ich wollte meinen Kaffeevollautomat via Siri-Sprachbefehl oder automatisiert einschalten können, so dass ich morgens nicht mehr darauf warten muss, bis die Maschine gestartet, gespühlt und augeheizt ist. Da mein Kaffeeautomat noch nicht sonderlich alt ist (vielleicht ein halben Jahr), wollte ich ihn aber auch nicht gleich durch ein (wahrscheinlich ziemlich teures) neues Modell mit Bluetooth-/App-Unterstützung eintauschen.

Stattdessen entdeckte ich den SwitchBot!

{{<figure src="foto1.jpeg" caption="Der SwitchBot ist ungefähr 3cm breit, 2cm tief und 1.5cm hoch.">}}

## SwitchBot: Macht jeden Schalter schlau

Der SwitchBot ist eigentlich ziemlich simpel: Es handelt sich im Endeffekt um einen kleinen Roboter mit einem "Arm", der sich dreht und dadurch einen Schalter automatisch betätigen kann. Man bringt also den SwitchBot neben dem zu betätigenden Schalter an, z. B. in dem man ihn mit dem mitgelieferten Klebepad festklebt und das war's.

Der SwitchBot wird dabei über Bluetooth mit der offiziellen SwitchBot-App gesteuert. Dies offenbart dann auch den ersten Nachteil der Geräte: Bluetooth hat  keine sehr hohe Reichweite. Wenn man also seine SwitchBots von "weiter weg" steuern möchte, dann benötigt man den SwitchBot Hub.

## Der SwitchBot Hub

{{<figure src="foto2.jpeg" caption="SwitchBot und SwitchBot Hub">}}

Der SwitchBot Hub bringt aber - abgesehen von Unabhängigkeit der Reichweite - noch weitere Vorteile:

* SwitchBots via WLAN bzw. Internet steuern
* Infrarot-Steuerung mit der z. B. Fernseher gesteuert werden können
* Erstellen von Siri Kurzbefehlen

Leider bringt der Hub auch einige Nachteile mit sich:

* Ein weiteres Hub-Gerät, das man irgendwo aufstellen muss (wenigstens kann es WLAN)
* Zusätzliche Kosten
* Nur verwendbar mit Online-Account bei SwitchBot

Insbesondere der letzte Punkt könnte ein No-Go für manche Leute sein. Ich sehe das da nicht so eng und man kann ja erfundene Daten beim Registrieren angeben.

Cool am Hub ist, dass dieser Infrarot-Steuerung mitbringt. Ich habe ihn z. B. direkt unter meinem Fernseher platziert. So kann ich nun auch noch meinen noch-nicht-ganz-so-smarten Fernseher (weil älter) mit Siri Shortcuts ein- und ausschalten.

## Die schlaue Kaffeemaschine

Wie sich herausstellte, war es gar nicht so einfach die SwitchBots hier in Deutschland zu bestellen. Mittlerweile sind sie wieder bei Amazon bestellbar, als ich gesucht hatte, war dem nicht so.

Endlich erhalten klebte ich den Bot an meine Kaffeemaschine und begann die Einrichtung. Diese gestaltete sich etwas komplexer als bei anderen SmartHome-Geräten, die SwitchBot-App ist leider nicht ganz so selbsterklärend wie viele andere SmartHome-Apps. Der Hersteller bietet aber einige Erklärvideos auf seiner Webseite an, mit deren Hilfe die Einrichtung schlussendlich trotzdem relativ schmerzlos möglich war.

Direkt nach der Einrichtung, konnte der SwitchBot einfach nur mit der App via Bluetooth gesteuert werden. Damit eine weitreichendere Steuerung möglich ist, muss zuerst der SwitchBot Hub installiert werden.

Auch die Einrichtung des Hubs gestaltete sich nicht als selbsterklärend, mit Hilfe der Herstellererklärungen aber einfach machbar. Auch für das Hinzufügen der Infrarot-Steuerung musste ich die Erklärungen des Herstellers konsultieren.

{{<figure src="screen1.jpeg" caption="Screenshot der SwitchBot-App nach der initialen Einrichtung">}}

Nachdem nun alles eingerichtet und mit der App steuerbar war, musste ich herausfinden, wie ich nun Siri beibringen kann, den Kaffeemaschinen-SwitchBot zu aktivieren. Die Antwort lautete: Siri Kurzbefehle.

Dazu muss der gewünschte Bot in der Übersicht aus dem Screenshot oben ausgewählt werden und anschließend in den Einstellungen des Bots die Cloud-Services aktiviert werden. In den Einstellungen der Cloud-Services hat man dann die Möglichkeit, eine Verbindung zu Google Assistant, Amazon Alexa, IFTT oder –für mich relevant – zu Siri Shortcuts herzustellen.

Die App installiert nun ein Siri Shortcut und schon kann ich Siri sagen "Kaffemaschine ein". Dies geht sogar auf dem Homepod.

{{<video "video.mp4">}}

## Fazit 

Da die Verbindung zu Siri auf Shortcuts basiert, ist sie leider auch "personenspezifisch". Der Kurzbefehl ist mit meinem Account verknüpft, womit es meiner Frau leider nicht möglich ist, den SwitchBot ebenfalls mittels Sprachbefehl auszulösen. Damit das ginge, müsste die App ebenfalls auf ihrem iPhone installiert werden und der Shortcut dort ebenfalls eingerichtet werden.

Insgesamt sind die SwitchBots eine spannende Möglichkeit, "dumme" Schalter schlau zu machen. Die rund 30€ pro SwitchBot empfinde ich als fairer Preis, die Funktionalität ist genau wie beworben. Die Account-Pflicht ist etwas nervig, für mich aber kein No-Go. Zusammen mit dem Hub (ebenfalls 35€) können spannende Automatisierungen eingerichtet werden, wie zum Beispiel die eingangs erwähnte Möglichkeit, beim Ausschalten des Weckers direkt die Kaffeemaschine einzuschalten.

Ein weiterer Nachteil ist, dass die SwitchBots nicht einfach in Home Assistant integriert werden können. Zwar gibt es eine Integration, allerdings läuft diese nur über Bluetooth. Der Hub selbst – und damit die meisten Automationsfunktionen – kann nicht mit Home Assistant verbunden werden.

Diesen Negativpunkten steht dafür gegenüber, dass mit Hilfe der SwitchBots für verhältnismäßig wenig Geld alle Dinge, die durch Schalter bedient werden, schlau und fernsteuerbar gemacht werden können. Auch wenn es besser ginge, so ist das doch schon ganz praktisch.

Und so habe ich mein Ziel erreicht. Eine persönliche Automation in der Siri Kurzbefehle-App fragt mich morgens, nachdem ich meinen Wecker ausschaltete, ob ich die Kaffeemaschine einschalten möchte. Ich tippe auf "Ok", gehe duschen und wenn ich in die Küche komme, ist die Kaffeemaschine bereit, meinen Kaffee zuzubereiten. Fast perfekt!