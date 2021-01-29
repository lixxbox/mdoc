# Mainsail App

Über [https://my.mainsail.app](https://my.mainsail.app/) kannst du immer die aktuellste Version von Mainsail abrufen.   
Dabei werden allerdings nur die statischen .html, .js und .css Dateien in deinen Browser-Storage geladen. Es werden keine weiteren Informationen an den Server übertragen. Die Kommunikation zu deinem Drucker erfolgt dann lokal direkt zwischen deinem Browser und deiner Moonraker Installation.   
Die Dateien werden auf github gehostet. Der Code kann also jederzeit unter [https://github.com/meteyou/mainsailAPP](https://github.com/meteyou/mainsailAPP) überprüft werden. Solltest du Bedenken haben, kannst du Mainsail natürlich auch weiterhin lokal auf deiner Hardware installieren. Ein Parallelbetrieb ist ebenfalls möglich.

Um Mainsail App verwenden zu können, müssen folgende Voraussetzungen erfüllt sein:

* Klipper muss installiert sein.
* Moonraker muss installiert sein.
* [my.mainsail.app](https://my.mainsail.app/) muss als CORS-Domain in der moonraker.conf eingetragen sein.

Die Einrichtung eines Webservers für Mainsail auf deiner Hardware entfällt somit. Ein weiterer Vorteil ist, dass mehrere Drucker eingerichtet werden können.

Die einfachen Installationsvarianten wären, entweder ein [MainsailOS](https://github.com/raymondh2/MainsailOS) Image zu verwenden, oder ein Helper-Skript wie z.B. [KIAUH](https://github.com/th33xitus/kiauh) zu verwenden.

Hier erklären wir dir aber, wie du es manuell Einrichtest.

