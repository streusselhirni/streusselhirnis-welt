---
title: "Hyperlinks in Markdown: Wie ich's mir endlich merken konnte"
date: 2022-05-23T21:40:36+02:00
draft: false
cover:
    image: header.png
---

Markdown ist eine sogenannte "Auszeichnungssprache". Dabei wird die Formatierung eines Textes sozusagen direkt mit Hilfe von Sonderzeichen in den Text integriert. Dies ermöglicht es einem Schreiber, schnell und einfach bereits während dem Verfassen eines Textes einfache Formatierungen vorzunehmen.

Hier einige Beispiele: Um in einem Markdown-Format etwas fett zu schreiben, muss man den fetten Text einfach in ** einpacken: ** Das hier wird fett **.

Oder Überschriften: Je nach Level der Überschrift (1. Ebene, 2. Ebene, ...) beginnt man seinen Titel einfach mit einem oder mehreren Raute-Symbolen:

```
# Dies ist die erste Überschrift

## Dies wird die zweite

et cetera.
```

## Hyperlinks
Und dann sind da Links. Um einen Link in Markdown zu setzen, muss man zuerst den Text, der anklickbar ist in runden Klammern und danach die URL in eckigen Klammern... oder was es umgekehrt?

## Eselsbrücke für Programmierer und Leute, die wissen, was Funktionen sind

Für Programmierer – oder all jene, die wissen, was Funktionen sind und wie diese aufgerufen werden – entdeckte ich mittlerweile eine praktische Eselsbrücke: Man muss einfach an einen Funktionsaufruf denken, als gäbe es die Funktion `createMarkdownLink()`.

So wird ganz schnell klar, dass der Syntax `[Ich bin der anklickbare Text](https://hier-url-einfuegen)` sein muss.
Denn `(Ich bin Text)[https://url]` wäre irgendein komischer Array-Zugriff auf einen Text und das macht keinen Sinn.

## Visuelle Eselsbrücke

Eine andere Variante ist, sich das ganze visuell vorzustellen:

`[TEXT](URL)` oder `(TEXT)[URL]`? Wenn wir uns folgendes Bild ansehen, dann wird relativ schnell klar, welche Variante stimmen muss:

{{<figure src="visuell.png" caption="Quelle: [Yumalnaura auf Github](https://gist.github.com/YumaInaura/eaa2ebab449ee4984bebcadf2270bbbb)">}}

## Wozu ist Markdown überhaupt gut?

Markdown wird unter anderem in verschiedensten Notiz-Programmen verwendet. Dort hilft es dir, beim Schreiben von Notizen diese sofort einigermaßen angenehm zu formatieren, so dass man sie später einfacher lesen kann.

Die besten mir bekannten Notiz-Apps, die Markdown unterstützen sind:

* [Obsidian](https://obsidian.md/) (Windows, Mac, iOS, iPad, Android)
* [Bear](https://bear.app/) (Mac, iOS, iPad)
* [Draft](https://getdrafts.com/) (Mac, iOS, iPad)
* [Notion](https://www.notion.so/) (Windows, Mac, iOS, iPad, Android)

Persönlich nutze ich Obsidian, eine völlig neue Art, Notizen zu erstellen. Aber das ist ein Thema für den nächsten Post. Welche Notiz-App nutzt ihr und verwendet ihr dort regelmäßig Markdown? Habt ihr eure eigene Methode, Markdown-Syntax zu merken? Lasst es mich wissen!