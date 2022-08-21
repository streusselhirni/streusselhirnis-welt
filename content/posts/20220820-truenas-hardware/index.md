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

Bis anhin waren diese Daten auf einer QNAP-NAS mit zwei 4TB Festplatten gespeichert. Diese ist nun leider zu alt, erhält keine Updates mehr und fällt in letzter Zeit mit Fehlern auf. Zeit also, für etwas Neues. Durch einige Videos von [Linus Tech Tips](https://www.youtube.com/channel/UCXuqSBlHAE6Xw-yeJA0Tunw) wurde ich an das NAS-Betriebssystem TrueNAS erinnert - und war sofort überzeugt. Es wird Zeit, für eine NAS Marke Eigenbau!

Einfache Consumer-NAS-Systeme vn Synology und QNAP leiden heutzutage an denselben Update-Obdoleszenz-Problemen wie moderne Smartphones: Irgendwann sagen die Hersteller "Dieses System ist zu alt, es gibt keine Updates mehr" und dann gibt die NAS langsam immer wie mehr die Funktion auf. Es wird also Zeit, meine QNAP zu ersetzen. Und zwar durch eine NAS Marke Eigenbau! Was TrueNAS ist, welche Vorteile es bietet und wie ihr auch zu einer solchen Custom-NAS kommen könnt, erzähle ich in dieser Serie!