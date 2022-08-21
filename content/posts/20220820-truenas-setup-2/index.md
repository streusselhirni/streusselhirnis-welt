
---
title: "TrueNAS - Teil 2: Installation"
date: 2022-08-19T19:04:04+02:00
draft: true
# cover:
#     image: "header.jpeg"
---

## Notizen

TrueNAS installer heruntergeladen und auf USB Stick gepackt: https://www.truenas.com/download-truenas-core/
Zur Installation von USB-Stick gebootet, danach dem Wizard gefolgt: https://www.truenas.com/docs/core/gettingstarted/install/

Storage konfigurieren: https://www.truenas.com/docs/core/gettingstarted/storingdata/

Pool erstellen: https://www.truenas.com/docs/core/gettingstarted/storingdata/
- TrueNAS has Raid-z2 vorgeschlagen, ich habe es auf Raid-z geändert, weil mir 1x Disk Parität reicht.
Hinweis auf Pool-Konfigurationen: https://www.truenas.com/docs/core/coretutorials/storage/pools/poolcreate/

Datasets erstellen: https://www.truenas.com/docs/core/coretutorials/storage/pools/datasets/

Share erstellen: https://www.truenas.com/docs/core/gettingstarted/sharingstorage/
Zuerst müssen die Berechtigungen auf den Datasets gesetzt werden. Diese sind sehr offen, einfach Zugriff für alle.
Anschließend wird der Share erstellt.
Da Mac ebenfalls SMB kann, belasse ich es für den Anfang bei einem SMB-Share.

Danach SSH im TrueNAS->Services aktivieren, per SSH auf die QNAP verbinden und mit `rsync -rvzh /share/MD0_DATA/Multimedia root@192.168.178.11:/mnt/box/media` den sync starten.
Damit der Rsync Task weiterläuft, auch wenn die SSH-Verbindung beendet wird, ab besten in einer `screen` Instanz laufen lassen.