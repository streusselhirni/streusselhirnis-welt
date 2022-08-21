---
title: "Zurück aus der Versenkung / Meet Hugo"
date: 2022-08-17T18:42:00+02:00
draft: false
cover:
   image: "hugo-logo.svg"
---

Lange habe ich mich nicht mehr gemeldet, jetzt bin ich zurück und das in neuer Gestalt! In der Zwischenzeit ist viel geschehen, unter anderem habe ich von Ghost zu Hugo gewechselt.

<!--more-->

Nachdem ich nun einige Wochen gesundheitsbedingt abwesend war, bin ich endlich zurück! In der Zwischenzeit habe ich eine ganze Sammlung von Ideen gesammelt, über die ich schreiben möchte, jetzt muss ich nur noch die Zeit finden, alles niederzuschreiben. Und für manche Blogeinträge wird auch etwas Recherche nötig sein. 😃

Doch zuerst zum Offensichtlichsten: Wie dir sicher aufgefallen ist, erstraht der Blog in einem neuen Design. Dies liegt daran, dass ich mein verwendetes Blog-System geändert habe! Der bisherige Blog lief über [Ghost](https://ghost.org/). Dabei handelt es sich um ein NodeJS-basiertes Blogging-System mit einem Fokus auf das, was einen Blog ausmacht - das Schreiben. Zusätzlich sind einige "community-building" Features eingebaut, wie das Versenden von Newslettern oder die Möglichkeit bezahlte Abonemente anzubieten inklusive Anbindung an Stripe (einen Zahlungsanbieter).

Der große Nachteil für mich war aber die Basis von Ghost: Die SaaS-Variante war mir zu teuer, also entschied ich mich vor ein paar Monaten den Blog auf einem VPS bei [Hetzner](https://hetzner.com) selbst zu hosten. Dies, weil das die günstigste Variante für NodeJS-Hosting ist – allerdings auch die aufwändigste. Nachdem ich dann letztens auch noch daran gescheitert bin, den Blog auf die neueste Version zu aktualisieren, habe ich es aufgegeben und mich dafür entschieden, alle Blogeinträge in ein neues System zu kopieren.

## Static Site Generation

Meine Anforderungen an ein neues System waren simpel: Man sollte einfach neue Beiträge schreiben können und es sollte leicht zu managen und günstig im Hosting sein. Der zweite Punkt führte mich entweder zu "klassischen" PHP-basierten Systemen wie WordPress (von de, ich absolut kein Fan bin), welches schon wieder viel mehr kann, als ich brauche, oder zu den so genannten Static Site Generatoren. Kleine Programme, die eine lokale Ordnerstruktur scannen und dann statische HTML-Seiten daraus generieren. Der Vorteil dieses Setups ist, dass der gesamte Inhalt des Blogs mit einer Versionsverwaltung wie Git gemanaged werden kann. Dank Git kann dann auch direkt eine Art "Online-Backup" des Blogs gepflegt werden, in dem man einfach ein Repository auf [Github](https://github.com) oder bei einem ähnlichen Anbieter verwendet.

Der Static Site Generator läuft dann als lokal installiertes Programm. Er scannt die Ordnerstruktur und Dateien und generiert die statischen Dateien. Diese können dann mit Git auf ein Repository bei Github gepusht werden. Und jetzt kommt das Coole: All dies bisher ist kostenlos. Wenn man nun schon eine Domain hat (diese kostet jedoch Geld), dann kann man z.B. mit Github Pages oder - in meinem Falle - mit Cloudflare Pages diese statischen HTML-Seiten sogar kostenlos im Internet hosten. So kostet mich das neue Blog-Setup quasi keinen Cent mehr (denn die Domain habe ich sowieso)!

## Meet Hugo

Doch welchen statischen Seitengenerator sollte ich verwenden? Hier gibt es einige: Hugo, Gatsby, NextJS, Jekyll, uvm. Ich wollte etwas, dass möglichst einfach installiert und bedienbar ist und im besten Falle noch schnell läuft. Aus letzterem Grund habe ich die meisten NodeJS-basierten Generatoren von vorneherein ausgeschlossen (außer Gatsby, den schloss ich aus, weil ich im Moment keine Lust habe, React zu lernen).

Schlussendlich gewann Hugo. Da dieser Generator in Go geschrieben ist, verspricht er sehr schnelle Laufzeiten und all meine Recherche deutete darauf hin, dass Hugo einfach zu installieren und einfach zu verwenden ist. Außerdem packt Hugo standardmäßig keinerlei JavaScript oder sonstigen Bloat in die fertigen HTML-Seiten. Dies kommt der Geschwindigkeit der finalen Webseite zu Gute.

Huge konnte ich auf meinem MacBook denktbar einfach installieren: `brew install hugo`. Das war's schon. Mit den passenden "Create-Befehlen" war dann auch die grundlegende Ordnerstruktur aufgebaut und ich konnte loslegen, alle meine bisherigen Blogposts zu migrieren. Glücklicherweise waren das noch nicht sehr viele, denn ich musste alle manuell von Hand kopieren!

## Wie neue Blogposts online kommen

Mit Hugo einen neuen Post, wie diesen hier, zu erstellen, ist denkbar einfach. Ich erstelle einfach im Blog-Ordner für jeden Post einen neuen Ordner mit einer Markdown-Datei, schreibe meinen Text und tadaa: Der Post ist fertig. Nun muss er nur noch online kommen. Doch wie kann ich das jetzt kostenlos online hosten?

Seit einiger Zeit habe ich all meine Domains zu Cloudflare migriert. Cloudflare ist einer der weltweit größte Anbieter für CDNs, Zero Trust Access-Lösungen, DNS-Dienste und seit nicht allzu langer Zeit auch als Registrar zu nutzen. Einer der Angebote von Cloudflare ist Cloudflare Pages, welches einem ermöglicht, kostenlos einfache, statische HTML-Seiten zu hosten.

Zusätzlich unterstützt Pages eine Art Continuous Integration: Da Cloudflare Pages auf einem Git-Repository basieren, "merkt" Cloudflare es, wenn es dort ein Update gibt und kann dann verschiedene Build-Vorgänge starten – z.B. das Generieren der statischen Seiten von Hugo.

Das Setup sieht also am Ende so aus, dass ich lokal einen neuen Post schreibe, die Änderungen dann in mein Github-Repository pushe, Cloudflare bemerkt dies, startet automatisch den `hugo` Build-Vorgang und sorgt anschließend dafür, dass die statischen HTML-Seiten online gehostet sind. Und das alles kostenlos!