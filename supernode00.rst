Das Blech
=========

Wir treiben ziemlich fiese Dinge mit unseren Servern; CPU und Netzwerktraffic (Volumen und Pakete-Rate) sind die entscheidenden Faktoren.

Voraussetzungen
---------------

Folgendes sollte euer Wunschserver leisten, damit er für FF tauglich ist:

* 100 Mbit garantierte Bandbreite

  * Nicht 100 Mbit Anbindung oder Peak Bandbreite! Der Server muss 24/7 100 Mbit abkönnen.

* Vollen Zugriff aufs Blech / den Hypervisor

  * Server neu installieren
  * Hardware reboot
  * IPs hinzufügen

* Leistungsstarke CPU

 * KVM Virtualisierung benötigt VT-x / VT-V Unterstützung der CPU
 * Geeignete CPUs sind z.B.:
  
   * Intel Xeon W
   * Intel Xeon E
   * AMD Opteron
   
 * Ungeeignete CPUs
 
   * Intel Pentium D
   * Intel Atom
   * AMD E350
   * ARM CPUs
 
* Zusätzliche IPv4 Adressen (Failover IPs) "zu Einmal-Kosten"


Folgendes sind absolute Ausschlusskriterien für einen Server:

* Trafficbegrenzung
* Fair use
* Vserver

Hoster / Rechenzentrum
----------------------

OVH bzw. deren preiswertere Marke "Soyoustart" (SYS) sind gut geeignet.

Die auf "OVH" gebrandeten Server leisten kaum mehr als die SYS Maschinen, kosten aber unverhältnismäßig viel mehr.

Bestellvorgang
--------------

Wer bei OVH oder SYS die Server bestellt sollte, wenn er Neukunde ist, per Überweisung zahlen. Das erspart zusätzliche Authentifizierungsmethoden und geht daher schneller(!) als Paypal.

Sicherheit
----------

Über das OVH/SYS Kundeninterface hat man die Möglichkeit den Server neu zu starten, neu zu installieren oder in den RescueMode zu booten. Man sollte daher dringend den Zugang zum Kundeninterface mit einer Two-Factor Login Methode zusätzlich absichern. Man kann die selbe OATH App nutzen, die man auch für Github und später das Proxmox Webinterface verwenden kann.

Für iOS wurde z.B. die App "OTP Auth" getestet. Auf Ubuntu-Phone lässt sich die App "Authenticator" einsetzen.
