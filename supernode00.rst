Das Blech
=========

Wir treiben ziemlich fiese Dinge mit unseren Servern; CPU und Netzwerktraffic (Volumen und Pakete-Rate) sind die entscheidenden Faktoren.

Vorraussetzungen
----------------

Folgendes sollte euer Wunschserver leisten, damit er für FF tauglich ist:

* 100 Mbit garantierte Bandbreite
  * Nicht 100 Mbit Anbindung oder Peak Bandbreite! Der Server muss 24/7 100 Mbit abkönnen.
* Vollen Zugriff aufs Blech / den Hypervisor
  * Server neu installieren
  * Hardware reboot
  * IPs hinzufügen
* Leistungsstarke CPU
* Zusätzliche IPv4 Adressen (Failover IPs) "zu Einmal-Kosten"


Folgendes sind absolute Ausschlusskriterien für einen Server:

+ Trafficbegrenzung
+ Fair use
+ Vserver

Hoster / Rechenzentrum
----------------------

OVH bzw. deren preiswertere Marke "Soyoustart" (sys) sind gut geeignet.

Die auf "OVH" gebrandeten Server leisten kaum mehr als die SYS Maschinen, kosten aber unverhältnismäßig viel mehr.


Bestellvorgang
--------------

Wer bei OVH oder SYS die Server bestellt sollte wenn er Neukunde ist per Überweisung zahlen, das erspart zusätzliche Authentifizierungsmethoden und geht daher schneller(!) als Paypal.

Sicherheit
----------

Über das OVH/SYS Kundeninterface hat man die Möglichkeit den Server neu zu starten, neu zu installieren oder in den RescueMode zu booten. Man sollte daher dringend den Zugang zum Kundeninterface mit einer Twofactor Login Methode zusätzlich absichern. Man kann die selbe OATH App nutzen, die man auch für Github und später das Proxmox webinterface verwenden kann.

