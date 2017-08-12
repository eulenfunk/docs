Server Kochbuch
===============

Anleitung zur Einrichtung eines Freifunk Supernodes auf Basis von Proxmox 5.0 und Ubuntu Server 16.04.2 LTS

Das Setup besteht im wesentlichen aus 3 Zonen:

* Die Freifunk Zone vor Ort (rosa): damit haben wir nicht viel zu tun.
* Die Serverzone (grün): um die geht es in dieser Anleitung.
* Das Backbone (orange), das macht der FFRL.

Die Serverzone teilt sich wiederum in 3 Segmente auf:

* Der Hypervisor Proxmox, dieser stellt alle Funktionen für den Betrieb von virtuellen Maschinen bereit.
* Der Konzentrator, dieser virtuelle Server stellt die Verbindung zu FFRL Backbone her, und übernimmt NAT und BGP.
* Der Supernode stellt die Fastd VPN Verbindungen für die Router bereit, kümmert sich um Batman, DHCP und radvd.

.. image:: http://freifunk-mk.de/gfx/Eulenschema.png
----

Vom Client ins Internet gehen die Daten folgenden Weg (IPv4):

.. image:: http://freifunk-mk.de/gfx/Eulenschema2.png
----

Und das ist der Rückweg (IPv4):

.. image:: http://freifunk-mk.de/gfx/Eulenschema3.png
----

Weiterlesen:

.. toctree::
   :maxdepth: 1

   supernode00
   supernode01
   supernode02
   supernode03
   supernode04
