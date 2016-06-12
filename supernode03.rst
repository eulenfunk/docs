Supernode einrichten
--------------------

Der Supernode ist der Freifunkseitige unserer zwei Server. Er übernimmt die Adressvergabe per DHCP / Radvd, den Aufbau der Fastd Tunnel zu den Routern und Batman.

Der Supernode wird im Proxmox Webinterface angelegt indem man auf der linken Seite den Server auswählt und dann oben rechts auf 'Create VM' klickt.

.. image:: http://freifunk-mk.de/gfx/proxmox-6.png

Im Reiter 'General' eine Freie ID und einen Namen (meinestadt-1) festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-7.png

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-8.png

Im Reiter 'CD/DVD' das ISO Image auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-9.png

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 6GB begrenzen und als Format 'qcow2' wählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-10.png

Im Reiter 'CPU' einen Prozessorkern zuweisen. Type "host" (mehr Performance, weniger Portabilität).

.. image:: http://freifunk-mk.de/gfx/proxmox-11.png

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256-2048MB festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-12.png

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diese VM zu verwendenden öffentlichen IPv4 Adresse eintragen. Bridged Mode übernehmen wir so und vmbr0 auch diese.

.. image:: http://freifunk-mk.de/gfx/proxmox-13.png

Bestätigen und Anlegen, auswählen und anschließend starten.

.. image:: http://freifunk-mk.de/gfx/proxmox-14.png

.. image:: http://freifunk-mk.de/gfx/proxmox-15.png

Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden Verzögerung. Details lassen sich ausklappen.

Hinweis: Wenn das System später läuft, nicht vergessen, den Starttyp "at boot time" zu stellen und das CD-ROM-Laufwerk entfernen.

.. image:: http://freifunk-mk.de/gfx/proxmox-16.png

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM links auswählen und oben rechts starten und die Konsole öffnen

.. image:: http://freifunk-mk.de/gfx/proxmox-17.png

Deutsch als Sprache auswählen und nun Ubuntu Server installieren

.. image:: http://freifunk-mk.de/gfx/proxmox-18.png

.. image:: http://freifunk-mk.de/gfx/proxmox-19.png

Als Installationssprache jetzt nochmal Deutsch auswählen, die auswahl trotz unvollständiger Unterstützung bestätigen und als nächstes das Tastaturlayout auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-20.png

.. image:: http://freifunk-mk.de/gfx/proxmox-21.png

.. image:: http://freifunk-mk.de/gfx/proxmox-22.png

.. image:: http://freifunk-mk.de/gfx/proxmox-23.png

.. image:: http://freifunk-mk.de/gfx/proxmox-24.png

.. image:: http://freifunk-mk.de/gfx/proxmox-25.png

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die manuelle Netzwerkkonfiguration auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-26.png

.. image:: http://freifunk-mk.de/gfx/proxmox-27.png

.. image:: http://freifunk-mk.de/gfx/proxmox-28.png

Die IP zur mac ist beispielsweise die 555.666.777.888

.. image:: http://freifunk-mk.de/gfx/proxmox-29.png

Die Subnetzmaske von 255.255.255.0 bleibt in der Regel so

.. image:: http://freifunk-mk.de/gfx/proxmox-30.png

Die Gateway Adresse sollte man beim Rechenzentrum bekannt sein.

Bei einem großen Französichen RZ ist das IPv4 Gateway immer auf der 254, also 555.666.777.254

.. image:: http://freifunk-mk.de/gfx/proxmox-31.png

Als DNS geht z.B. der 8.8.8.8 von google.

.. image:: http://freifunk-mk.de/gfx/proxmox-32.png

Der Rechnername ist frei wählbar z.b. meinestadt-1

.. image:: http://freifunk-mk.de/gfx/proxmox-33.png

Der Domainname ist hier einzutragen

.. image:: http://freifunk-mk.de/gfx/proxmox-34.png

Und der Benutzername.

.. image:: http://freifunk-mk.de/gfx/proxmox-35.png

.. image:: http://freifunk-mk.de/gfx/proxmox-36.png

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

.. image:: http://freifunk-mk.de/gfx/proxmox-37.png

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png

Zeitzone prüfen und bestätigen.

Festplatte manuell formatieren

.. image:: http://freifunk-mk.de/gfx/proxmox-39.png

Freien Speicherplatz auswählen und Enter

.. image:: http://freifunk-mk.de/gfx/proxmox-40.png

Partitionstabelle erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-41.png

Freien Speicherplatz auswählen und Enter

.. image:: http://freifunk-mk.de/gfx/proxmox-42.png
.. image:: http://freifunk-mk.de/gfx/proxmox-43.png

Partitionsgröße 5 GB primär am Anfang

.. image:: http://freifunk-mk.de/gfx/proxmox-44.png
.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
.. image:: http://freifunk-mk.de/gfx/proxmox-46.png

Bootflag auf 'ein' setzen und 'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-47.png

Freien Speicherplatz auswählen und Enter

.. image:: http://freifunk-mk.de/gfx/proxmox-48.png

Einen neue Partition erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-49.png

Größe bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-50.png

Primär

.. image:: http://freifunk-mk.de/gfx/proxmox-45.png

Benutzen als 'Auslagerungsspeicher (SWAP)'

'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-51.png

'Partitionierung beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-52.png

Ja schreiben, noch sind ja keine Daten vorhanden, die überschrieben werden könnten.

.. image:: http://freifunk-mk.de/gfx/proxmox-53.png

Warten...

Proxy leer lassen

.. image:: http://freifunk-mk.de/gfx/proxmox-54.png

Warten...

Automatische Sicherheitsaktualisierungen auswählen

.. image:: http://freifunk-mk.de/gfx/proxmox-55.png

OpenSSH Server auswählen (Leertaste benutzen) und weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-56.png

Warten...

Die Installation des GRUB Bootloader bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-57.png

Weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-58.png

SSH
^^^

Per SSH mit dem Server verbinden

::

	ssh meinbenutzername@111.222.333.444

Den Public-Key für den User hinterlegen:

::

	        cd /home/meinbenutzername/
	        mkdir .ssh
	        nano .ssh/authorized_keys

Im Editor dann den Public Key ("ssh-rsa AAA.....") einfügen. Wichtig: Alles von diesem Key muss in eine Zeile.
Weitere Adminuser können später angelegt werden.

Nun das Password-Login auf dem Server deaktivieren. Dazu die sshd_config editieren:

::

	sudo nano /etc/ssh/sshd_config

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no

Achtung, auch wenn 'yes' auskommentiert ist, besteht die Möglichkeit sich per Password zu verbinden, erst wenn 'no' gesetzt ist und nicht (mehr) auskommentiert ist, ist der Zugriff nur noch per Key möglich.

Um es den Script-Kiddies und Bots etwas schwerer zu machen, sollte der Port 22 auf einen hohen Port (mindestens über 1024) verändert werden. Dazu die Zeile

::

	Port 22

ändern in

::

	Port 62954

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss.

Nun den direkten Rootlogin sperren.

::

	PermitRootLogin yes

ändern in

::

	PermitRootLogin no
	UsePAM no

Danach den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen.

::

	sudo service ssh restart

Den nachfolgenden ssh Kommandos muss man die Option "-p 62954" (kleines "p"!) und den scp Kommandos
die Option "-P 62954" (großes "P"!).

::

			ssh -p 62954 meinbenutzername@111.222.333.444

Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als Nächstes steht die Systemaktualisierung an; auch hier beim erstmaligen Aufruf die Nutzung von IPv4 erzwingen für's APT-Get

::

	sudo apt-get update
	sudo apt-get dist-upgrade
	sudo apt-get autoremove

Pakete installieren
^^^^^^^^^^^^^^^^^^^

Ergänzen der /etc/apt/sources.list um das fastd repository

::

	sudo nano /etc/apt/sources.list

Folgende Zeile hinzufügen

::

	deb http://repo.universe-factory.net/debian/ sid main

Editor schließen

::

	sudo apt-get update
	sudo apt-get install xinetd git vnstat vnstati gdebi-core lighttpd fastd build-essential \
	bridge-utils isc-dhcp-server radvd libnl-3-dev pkg-config

Rückfrage mit "J" bestätigen

Um welche Paket handelt es sich?

* vnstat monitort den Netzwerktraffic
* vnstati erzeugt daraus Grafiken
* lighttpd stellt diese zum Abruf bereit
* gdebi-core ermöglicht uns die Installation des Check_mk Agents
* xinetd ist der bei Debian übliche Super-Daemon, über ihn wird der Check_mk Agent angesprochen
* Fastd baut Tunnelverbindungen zu den Routern auf
* build-essential wird zum kompilieren von Batman benötigt
* bridge-utils (brctl) steuert Netzwerkbrücken
* isc-dhcp-server (dhcpd3) verteilt IPv4 Adressen
* radvd verteilt die IPv6 Range
* git wird für die Konfigurationsscripte benötigt
* libnl-3-dev wird für batman benötigt
* pkg-config wird für batctl benötigt


Batman kompilieren
^^^^^^^^^^^^^^^^^^

Batman kann man bei http://www.open-mesh.org/projects/open-mesh/wiki/Download herunterladen

::

	cd ~
	wget http://downloads.open-mesh.org/batman/stable/sources/batman-adv/batman-adv-2016.0.tar.gz
	tar -xf batman-adv-2016.0.tar.gz
	cd batman-adv-2016.0
	make
	sudo make install


Batctl kompilieren
^^^^^^^^^^^^^^^^^^

::

	cd ~
	sudo wget https://downloads.open-mesh.org/batman/stable/sources/batctl/batctl-2016.0.tar.gz
	tar -xf batctl-2016.0.tar.gz
	cd batctl-2016.0
	make
	sudo make install

Batman Kernelmodul eintragen
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Damit das Batman Kernelmodul beim boot geladen wird müssen wir es noch in die /etc/modules eintragen.

Mehr infos gibt es im ubuntuusers wiki https://wiki.ubuntuusers.de/Kernelmodule#start

::

	sudo nano /etc/modules

::

	# /etc/modules: kernel modules to load at boot time.
	#
	# This file contains the names of kernel modules that should be loaded
	# at boot time, one per line. Lines beginning with "#" are ignored.
	batman-adv

Fastd einrichten
^^^^^^^^^^^^^^^^
* Verzeichnis für die Fastd Instanz anlegen
* Dummyverzeichnis für Clients anlegen
* fastd.conf erstellen

::

	sudo mkdir -p /etc/fastd/client/dummy
	cd /etc/fastd/client
	sudo nano fastd.conf

::

	bind any:10000 default ipv4;
	include "secret.conf";
	include peers from "dummy";
	interface "tap0";
	log level info;
	mode tap;
	method "salsa2012+umac";
	peer limit 200;
	mtu 1406;
	secure handshakes yes;
	log to syslog level verbose;
	status socket "/run/fastd.client.sock";

	on up "
			ip link set address 04:EE:EF:CA:FE:3A dev tap0
			ip link set up tap0
			/usr/local/sbin/batctl -m bat0 if add $INTERFACE
			ip link set address 02:EE:EF:CA:FE:FF:3A dev bat0
			ip link set up dev bat0
			brctl addif br0 bat0
			/usr/local/sbin/batctl -m bat0 it 5000
			/usr/local/sbin/batctl -m bat0 bl 0
			/usr/local/sbin/batctl -m bat0 gw server 48mbit/48mbit
			/usr/local/sbin/batctl -m bat0 vm server
	";

	on verify "/etc/fastd/client/blacklist.sh $PEER_KEY";

Nun das Blacklist-Script anlegen.

::

	sudo nano /etc/fastd/client/blacklist.sh

Mit Inhalt:

::

	#!/bin/bash
	PEER_KEY=$1
	echo peer "$PEER_KEY" joining
	if /bin/grep -Fq $PEER_KEY /etc/fastd/client/fastd-blacklist.json; then
        exit 1
	else
        exit 0
	fi

dann die Datei ausführbar machen

::

	sudo chmod +x  /etc/fastd/client/blacklist.sh

Und schließlich eine Dummy-Datei anlegen

::

	sudo nano /etc/fastd/client/fastd-blacklist.json

dort hinein

::

	{
	"peers":
  	[
        {
        "pubkey":"0004df72c02827333bced7680acaf38f36b09597c55241571e90637465831000",
        }
	]
	}


Den Editor wieder verlassen und nun einen fastd Key erzeugen, der in passender Syntax in "secret.conf" abgelegt wird.

::

	sudo fastd --generate-key > secret.conf

In der Datei secret.conf müssen dann manuell Änderungen vorgenommen werden:
Die Zeile mit 'Public' muss mit '#' auskommentiert werden, die Zeile 'Secret' muss angepasst werden.

::

	sudo nano secret.conf

::

	secret "xxx...";
	#Public: ...



Hinzufügen einer Schnittstelle eth1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nun muss im Proxmox für die VM eine eth1 hinzugefügt werden, die auf der vmbr1 hängt und Virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die VM einmal durchbooten.


Verbindung zwischen Supernode und Konzentrator konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Auf dem Supernode
.................

Zunächst müssen die nötigen Scripte auf den Supernode heruntergeladen und ausführbar gemacht werden:

::

	sudo mkdir -p /opt/eulenfunk
	cd /opt/eulenfunk
	sudo git clone https://github.com/eulenfunk/supernode.git
	cd supernode
	sudo chmod +x *.sh
	sudo chmod +x *.py


Nun muss man dem jeweiligen Supernode aus dem vom FFRL zugeteilten IPv6-Adressbereich noch ein /56 herausschneiden, ein passendes
IPv4 Netz für seine Endgeräte festlegen und die Werte in die Konfigurationsdatei supernode.config schreiben:

::

	sudo nano /opt/eulenfunk/supernode/supernode.config


Hier ein Beispiel:

::

	SUPERNODE_IPV6_PREFIX=2a03:2260:X:Y::/56
	SUPERNODE_IPV4_CLIENT_NET=172.19.0.0/16
	SUPERNODE_IPV4_TRANS_ADDR=172.31.254.1


Die angepasste Konfiguration wird dann durch das Setup verwendet:

::

	cd /opt/eulenfunk/supernode
	sudo ./supernode-setup.sh


::

	Ausgaben in:
		interfaces.eulenfunk
		dhcpd.conf.eulenfunk
		radvd.conf.eulenfunk
		20-ff-config.conf.eulenfunk

Die so erzeugten Konfigurationsdateien müssen **nach Prüfung** an die passenden Stellen kopiert werden

::

	sudo cp dhcpd.conf.eulenfunk /etc/dhcp/dhcpd.conf
	sudo cp radvd.conf.eulenfunk /etc/radvd.conf
	sudo cp 20-ff-config.conf.eulenfunk /etc/sysctl.d/20-ff-config.conf

und die Netzwerkkonfiguration an die vorhandene angehängt werden:

::

	sudo cat interfaces.eulenfunk >> /etc/network/interfaces

Als letzter Schritt auf dem Supernode muss die /etc/rc.local folgendermassen angepasst werden:

::

	sudo nano /etc/rc.local


::

	#!/bin/sh -e
	#
	# rc.local
	#
	# This script is executed at the end of each multiuser runlevel.
	# Make sure that the script will "exit 0" on success or any other
	# value on error.
	#
	# In order to enable or disable this script just change the execution
	# bits.
	#
	# By default this script does nothing.

	/opt/eulenfunk/supernode/supernode-rc.sh

	exit 0


Das sorgt dafür, dass beim Systemstart durch das Script supernode-rc.sh die nötigen Routen und Routing-Policies konfiguriert werden.

Optional: dhcp-server einmal täglich neu starten
................................................

Der ISC-DHCP hat die unangenehme Eigenschaft (zumindest in der mit Ubuntu derzeit ausgelieferten Version), Die Datei mit den aktiven dhcp-Adressen nicht automatisch zu reorganisieren. Das stört zwei eigentlich nicht in Bezug auf die Performance des Dienstes.
Die /etc/dhcp/dhcpd.leases kann jedoch viele (viele!) MB groß werden und wenn man dann mit Tools darauf schauen möchte, um nach den noch aktiven Leases zu suchen, dann kostet das CPU und IO, diese Datei jeweils komplett einzulesen und durchzusortieren. Daher ist es ratsam, den DHCP-Server zumindest einmal täglich neu durchzustarten, da er dabei automatich sein Lease-file reorganisiert. 

Nachteil: Wärend dieser 1-5 Sekunden werden Clients keine DHCP-Requests beantwortet bekommen. ("Eingeschränkte Connektivität")

::

	sudo echo "#ISC-DHCP neu starten, einmal täglich um 4h29" >/etc/cron.d/dhcprestart
	sudo echo "29 4 * * * 	root /etc/init.d/isc-dhcp-server restart">>/etc/cron.d/dhcprestart
	

Optional: dhcpleaes-script installieren
---------------------------------------

::

	sudo mkdir /opt/eulenfunk
	cd /opt/eulenfunk
	wget https://raw.githubusercontent.com/eulenfunk/scripts/master/dhcpleases
	sudo chmod +x dhcpleases



Check_MK Agent installieren
...........................

Den Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit:

In die CheckMK-Instanz per Webbrowser einloggen. Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.2.8p1-1_all.deb _(Beispiel)_

Den Download-Link in die Zwischenablage kopieren.
Im SSH-Terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget --no-check-certificate \
        https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/check-mk-agent_1.2.8p1-1_all.deb

Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum Ausliefern der Monitoring Daten.

Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	sudo gdebi check-mk-agent_1.2.8p1-1_all.deb

Anschließend noch das Supernode-Plugin hinzufügen:

::

	cd /usr/lib/check_mk_agent/local
	sudo wget -O supernode https://raw.githubusercontent.com/eulenfunk/check_mk/master/supernode
	sudo chmod 755 supernode
	sudo chmod +x supernode

Der Rechner hält ab nun Daten zum Abruf bereit.

JJX Bescheid sagen, der kümmert sich dann darum.



Danach den Supernode rebooten.

Hier eine grafische Übersicht über die beteiligten Konfigurationsdateien auf dem Supernode:

.. image:: https://raw.githubusercontent.com/eulenfunk/supernode/master/Supernode-Routing.png

Auf dem Konzentrator
....................

Auf dem Konzentrator muss die zum Supernode passende Konfiguration angelegt werden:


::

	cd /opt/eulenfunk/konzentrator/config
	sudo nano meinestadt-1

::

Dort müssen folgende Werte eingetragen werden:

::

	# Beschreibender Name "stadt-N"
	SUPERNODE_NAME=meinestadt-1

	# Soll die Netzwerkkonfiguration automatisch beim Systemstart gesetzt werden
	AUTOSTART=1

	# IPv4 Konfiguration
	SUPERNODE_CLIENT_IPV4_NET=<IPv4 Netz fuer die Clients, 172.XX.0.0/16>
	SUPERNODE_TRANS_IPV4_NET=<IPv4 Transit-Netz, 172.31.YYY.0/24>
	SUPERNODE_TRANS_IPV4_REMOTE=<Supernode IPv4 eth1 Adresse Transit-Netz, 172.31.YYY.1>

	# IPv6 Konfiguration
	SUPERNODE_CLIENT_IPV6_NET=<IPv6 Netz fuer die Clients, 2a03:2260:AAAA:BBBB::/64>
	SUPERNODE_TRANS_IPV6_NET=<IPv6 Supernetz fuer Transit, 2a03:2260:AAAA:BBBB::/56>
	SUPERNODE_TRANS_IPV6_LOCAL=<IPv6 Supernetz lokale Adresse, 2a03:2260:AAAA:BBBB::1>
	SUPERNODE_TRANS_IPV6_REMOTE=<IPv6 Supernetz remote Adresse, 2a03:2260:AAAA:BBB::2>


Man kann dann die Konfiguration folgendermaßen aktivieren:

::

	cd /opt/eulenfunk/konzentrator
	sudo ./supernode.sh start meinestadt-1


Die Konfiguration kann im laufenden Betrieb auch wieder entfernt werden (damit wird die Stadt allerdings vom Freifunk getrennt!)

::

	cd /opt/eulenfunk/konzentrator
	sudo ./supernode.sh stop meinestadt-1


Durch den Parameter AUTOSTART=1 wird beim Reboot des Konzentrators die Konfiguration für diese Stadt automatisch wieder gesetzt.

Den Konzentrator und den Supernode rebooten, um die Reboot-Festigkeit zu testen.
