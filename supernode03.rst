Supernode einrichten
--------------------

Der Supernode ist der Freifunkseitige unserer zwei Server. Er übernimmt die Adressvergabe per DHCP / Radvd, den Aufbau der Fastd Tunnel zu den Routern und Batman.

Der Supernode wird im Proxmox Webinterface angelegt indem man auf der linken Seite den Server auswählt und dann oben rechts auf 'Create VM' klickt.

.. image:: http://freifunk-mk.de/gfx/proxmox-6.png

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-7.png

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-8.png

Im Reiter 'CD/DVD' das ISO Image auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-9.png

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 8GB begrenzen und als Format 'qcow2' wählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-10.png

Im Reiter 'CPU' zwei Prozessorkerne zuweisen.

.. image:: http://freifunk-mk.de/gfx/proxmox-11.png

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 -1024MB festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-12.png

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diesen Vserver zu verwendenden öffentlichen IPv4 Adresse eintragen.

.. image:: http://freifunk-mk.de/gfx/proxmox-13.png

Bestätigen und Anlegen, auswählen und anschließend starten.

.. image:: http://freifunk-mk.de/gfx/proxmox-14.png

.. image:: http://freifunk-mk.de/gfx/proxmox-15.png

Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden verzögerung. Details lassen sich ausklappen. Auf einigen Systemen ist es notwendig, die Harddisk auf "Writeback(insecure)" zu schalten, um das System zu starten zu können.

Hinweis: Wenn das System später läuft, nicht vergessen, den Starttyp "at boot time" zu stellen.

.. image:: http://freifunk-mk.de/gfx/proxmox-16.png

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM Links auswählen und oben rechts starten und die Konsole öffnen

.. image:: http://freifunk-mk.de/gfx/proxmox-17.png

Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

.. image:: http://freifunk-mk.de/gfx/proxmox-18.png

.. image:: http://freifunk-mk.de/gfx/proxmox-19.png

Als Installationssprache jetzt nochmal Deutsch auswählen, die auswahl trotz unvollständiger Unterstützung bestätigen und als nächstes das Tastaturlayout auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-20.png

.. image:: http://freifunk-mk.de/gfx/proxmox-21.png

.. image:: http://freifunk-mk.de/gfx/proxmox-22.png

.. image:: http://freifunk-mk.de/gfx/proxmox-23.png

.. image:: http://freifunk-mk.de/gfx/proxmox-24.png

.. image:: http://freifunk-mk.de/gfx/proxmox-25.png

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die Manuelle Netzwerkkonfiguration auswählen.

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

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den Persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png

Zeitzone Prüfen und bestätigen.

Festpaltte manuell formatieren

.. image:: http://freifunk-mk.de/gfx/proxmox-39.png

Freien speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-40.png

Partitionstabelle erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-41.png

Freien speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-42.png
.. image:: http://freifunk-mk.de/gfx/proxmox-43.png

Partitionsgröße 7 GB Primär am Anfang

.. image:: http://freifunk-mk.de/gfx/proxmox-44.png
.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
.. image:: http://freifunk-mk.de/gfx/proxmox-46.png

Bootflag auf 'ein' setzen und 'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-47.png

Freien Speicherplatz auswählen und enter

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

Openssh server auswählen (Leertaste benutzen) und weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-56.png

Warten...

Die Installation des GRUB Bootloader bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-57.png

Weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-58.png

SSH
^^^

Die weitere Konfiguration soll per SSH Zugriff erfolgen, daher richten wir diesen zuerst ein und sichern den SSH Server ab.

vom PC aus per SSH mit dem Server verbinden

::

	ssh root@555.666.777.888

Nun den SSH Public Key auf dem Server hinterlegen

::

	mkdir .ssh
	cd .ssh
	nano authorized_keys

In die noch leere Datei den Key eintragen und den Editor wieder verlassen.

Als nächstes die SSH Verbindung beenden

::

	exit

Und unter Verwendung des SSH Keys erneut verbinden

::

	ssh root@555.666.777.888

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.

Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@555.666.777.888

Nun den Password login auf dem Server deaktivieren, dazu die sshd_config editieren

::

	sudo nano /etc/ssh/sshd_config

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no
	UsePAM no

Achtung, auch wenn "yes" auskommentiert ist besteht die Möglichkeit sich per Password zu verbinden. Erst wenn "no" gesetzt ist und nicht auskommentiert ist, ist der Zugriff nur noch per Key möglich.

Um es den Script-Kiddies und Bots etwas schwerer zu machen, sollte der Port 22 auf einen hohen Port (mindestens über 1024) verändert werden. Dazu die Zeile

::

	Port 22

ändern z.B. in

::

	Port 62954

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss. Ändernt man diesen Port, muss dieser auch in der Ferm config (weiter unten beschrieben) geändert werden, da ferm sonst nur ssh auf Port 22 zu lässt.


Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen

::

	sudo /etc/init.d/ssh restart


Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als nächstes steht die Systemaktualisierung an, dafür einmal

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
	sudo apt-get install xinetd vnstat vnstati gdebi lighttpd fastd build-essential \
	bridge-utils isc-dhcp-server radvd python-pip gdebi xinetd

Rückfrage mit "J" bestätigen

Um welche Paket handelt es sich?

* vnstat monitort den Netzwerktraffic
* vnstati erzeugt daraus Grafiken
* lighttpd stellt diese zum Abruf bereit
* gdebi ermöglicht uns die Installation des Check_mk Agents
* xinetd übernimmt die Übertragung der Monitoring Daten
* Fastd baut Tunnelverbindungen zu den Routern auf
* build-essential wird zum kompilieren von Batman benötigt
* bridge-utils (brctl) steuert Netzwerkbrücken
* isc-dhcp-server (dhcpd3) verteilt IPv4 Adressen
* radvd verteilt die IPv6 Range
* python-pip um python-module nachinstallieren zu können

Batman kompilieren
^^^^^^^^^^^^^^^^^^

Batman kann man bei http://www.open-mesh.org/projects/open-mesh/wiki/Download herunterladen

Zur Vorbereitung libnl-3-dev installieren (Rückfrage mit "J" bestätigen)

::

	sudo apt install libnl-3-dev
	
::

	cd ~
	wget http://downloads.open-mesh.org/batman/stable/sources/batman-adv/batman-adv-2016.0.tar.gz
	tar -xf batman-adv-2016.0.tar.gz
	cd batman-adv-2016.0
	make
	sudo make install


Batctl kompilieren
^^^^^^^^^^^^^^^^^^

Zur Vorbereitung pkg-config installieren (Rückfrage mit "J" bestätigen)

::

	sudo apt-get install pkg-config
	
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
* Verzeichnis für die Fastd Instand anlegen
* Dummyverzeichnis für Clients anlegen
* fastd.conf erstellen

::

	cd /etc/fastd
	sudo mkdir client
	cd client
	sudo mkdir dummy
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

Nun das blacklist-script anlegen. 

::
	
	sudo nano /etc/fastd/client/blacklist.sh
	
mit Inhalt

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

	fastd --generate-key |sed s/Secret\:\ /#fastd-key\ \"$HOSTNAME\\nsecret\ \"/| \
	sed s/Public\:\ /#public\ \"/|sed s/\$/\"\;/>secret.conf


Hinzufügen einer Schnittstelle eth1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nun muss im Proxmox für die vm eine eth1 hinzugefügt werden, die auf der vmbr1 hängt und virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die vm einmal durchbooten.


Verbindung zwischen Supernode und Konzentrator konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Voraussetzung für diese Vorgehensweise ist die vorhergehende Konfiguration des BGP-Konzentrators mittels "ff-bgp-konzentrator-konfigurator".

Auf dem Supernode
.................

Die Konfiguration erfolgt mit Root-Rechten. Also wechseln wir für die nächsten Schritte zum User root:

::

	sudo -i

Zunächst müssen die nötigen Scripte auf den Supernode heruntergeladen und ausführbar gemacht werden:

::

	mkdir -p /opt/eulenfunk/supernode
	cd /opt/eulenfunk/supernode
	wget https://raw.githubusercontent.com/eulenfunk/scripts/master/supernode/supernode-setup.sh
	wget https://raw.githubusercontent.com/eulenfunk/scripts/master/supernode/supernode-rc.sh
	wget https://raw.githubusercontent.com/ffrl/ff-tools/master/fastd/fastd-statistics.py
	wget https://raw.githubusercontent.com/ffrl/ff-tools/master/fastd/fastdtop.py
	chmod +x *.sh
	chomd +x *.py
	ln /opt/eulenfunk/supernode/fastd-statistics.py /usr/sbin/fastd-statistics
	ln /opt/eulenfunk/supernode/fastdtop.py /usr/sbin/fastdtop
	pip install npyscreen hurry.filesize

	

Dann muss die Konfigurationsdatei supernode.config angepasst werden.

::

	nano /opt/eulenfunk/supernode/supernode.config

Nun muss man dem jeweiligen Supernode aus dem vom FFRL zugeteilten IPv6-Adressbereich noch ein /56 herausschneiden:

::

	SUPERNODE_IPV6_PREFIX=2a03:2260:120:300::/56
	SUPERNODE_IPV4_CLIENT_NET=172.19.0.0/16
	SUPERNODE_IPV4_TRANS_ADDR=172.31.254.1


Die angepasste Konfiguration wird dann durch für das Setup verwendet:

::

	./supernode-setup.sh


::

	Ausgaben in:
		interfaces.eulenfunk
		dhcpd.conf.eulenfunk
		radvd.conf.eulenfunk
		20-ff-config.conf.eulenfunk

Die so erzeugten Konfigurationsdateien müssen **nach Prüfung** an die passenden Stellen kopiert werden

::

	cp dhcpd.conf.eulenfunk /etc/dhcp/dhcpd.conf
	cp radvd.conf.eulenfunk /etc/radvd.config
	cp 20-ff-config.conf.eulenfunk /etc/sysctl.d/20-ff-config.conf

und die Netzwerkkonfiguration an die vorhandene angehängt werden:

::

	cat interfaces.eulenfunk >> /etc/network/interfaces

Als letzter Schritt auf dem Supernode muss die /etc/rc.local folgendermassen angepasst werden:

::

	nano /etc/rc.local


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


Check_MK Agent imstallieren
...........................

Den Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit:

In die CheckMK-Instanz per Webbrowser einloggen. Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.2.6p15-1_all.deb _(Beispiel)_

Den Download-Link in die Zwischenablage kopieren.
Im ssh-terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget --no-check-certificate \
        https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/check-mk-agent_1.2.6p15-1_all.deb
	gdebi check-mk-agent_1.2.6p15-1_all.deb

Anschließend noch das Konzentrator-Modul hinzufügen: 

::

	cd /usr/lib/check_mk_agent/local
	wget -O supernode https://raw.githubusercontent.com/eulenfunk/check_mk/master/supernode
	chmod +x supernode


Der Rechner hält ab nun Daten zum Abruf bereit.


_ToDo: Neuen Rechner im CheckMK eintragen in richtige Gruppe & Monitoring scharf schalten.
Alternativ JJX Bescheid sagen, der kümmert sich dann darum.




Danach den Supernode rebooten.

Hier eine grafische Übersicht über die beteiligten Konfigurationsdateien auf dem Supernode:

.. image:: https://raw.githubusercontent.com/eulenfunk/scripts/master/supernode/Supernode-Routing.png

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
	SUPERNODE_TRANS_IPV4_REMOTE=<Remote IPv4 Adresse Transit-Netz, 172.31.YYY.1>

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

Wenn möglich (wenn noch keine anderen Städte über den Konzentrator gehen), den Konzentrator rebooten.

Testen
......

... TBD ...
