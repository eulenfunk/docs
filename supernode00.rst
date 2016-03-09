Das Blech
=========

Wir treiben ziemlich fiese dinge mit unseren Servern, CPU und Netzwerktraffic sind die entscheidenden Faktoren.

Vorraussetzungen
----------------

Folgendes sollte euer Wunschserver leisten, damit er für FF Tauglich ist:

+ 100 Mbit garantierte Bandbreite
+ VOllen Zugriff aufs Blech / den Hypervisor
+ Leistungsstarke CPU
+ Zusätzliche IPv4 Adressen (Failover IPs)


Folgendes sind absolute Ausschlusskriterien für einen Server:

+ Trafficbegrenzung
+ Fair use
+ Vserver

Hoster / Rechenzentrum
----------------------

OVH bzw. deren preiswertere Marke Soyoustart (sys) sind gut geeignet.

Die OVH Server leisten kaum mehr als die SYS Maschinen, kosten aber unverhältnismäßig viel mehr.


Bestellvorgang
--------------

Wer bei OVH oder SYS die Server bestellt sollte wenn er Neukunde ist per Überweisung Zahlen, das erspart zusätzliche Authentifizierungsmethoden und geht daher schneller als Paypal.

Sicherheit
----------

Über das OVH/SYS Kundeninterface hat man die Möglichkeit den Server neu zu Starten, neu zu installieren oder in den rescue mode zu booten. Man sollte daher dringend den Zugang zum Kundeninterface mit einer Twofactor Login Methode zusätzlich absichern. Man kann die selbe OATH App nutzen, die man auch für Github und später das Proxmox webinterface verwnden kann.

