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

Den zugehörigen Schlüssel importieren

::

	sudo apt-key add - <<EOF
	-----BEGIN PGP PUBLIC KEY BLOCK-----
	Version: GnuPG v1

	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
	=XTaw
	-----END PGP PUBLIC KEY BLOCK-----
	EOF



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

Check_MK Agent installieren
...........................

Den Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit:

In die CheckMK-Instanz per Webbrowser einloggen. Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.2.8p11-1_all.deb _(Beispiel)_

Den Download-Link in die Zwischenablage kopieren.
Im SSH-Terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget https://monitoring.eulenfunk.de/eulenfunk/check_mk/agents/check-mk-agent_1.2.8p11-1_all.deb


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

::
		sudo nano /etc/xinetd.d/check_mk

Dort die Zeile

::

	# only_from = 127.0.0.1 10.0.20.1 10.0.20.2

ändern in

::

		only_from = 127.0.0.1 94.23.160.148

Damit diese Änderungen aktiviert werden, muss der xinetd durchgestartet werden

::

	sudo /etc/init.d/xinetd restart


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
