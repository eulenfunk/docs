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

	deb https://repo.universe-factory.net/debian/ sid main

Editor schließen

Den zugehörigen Schlüssel importieren

::

	sudo apt-key add - <<EOF
	-----BEGIN PGP PUBLIC KEY BLOCK-----
	Version: GnuPG v1

	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
	YXMgU2NoaWZmZXIgPG1zY2hpZmZlckB1bml2ZXJzZS1mYWN0b3J5Lm5ldD6JAlcE
	EwEKAEECGwMFCwkIBwMFFQoJCAsFFgMCAQACHgECF4ACGQEWIQRmZOe9prZpiB7F
	LnUW7z9kyyAdnAUCWHE2fQUJB4VIuAAKCRAW7z9kyyAdnGCVD/4gKvFknx5yHlcd
	bge08G4S7o+mWEvl0C1FefgvFaFbQ2QFDp5vsH4SBf8ldsbmOyMafzDCCqune4EP
	n0SsDGrMRWGuLaoPwHrODz2E/iZCk4owxtXOYM659eW2ua/PuwRmvnKU4t1cBjFw
	IB3ifWiSUY4L4oF4+xZTQdqVyTVaDvHcogXaIgKILfiOnLPk1mFlRPyxESJtG6bp
	vZBLLMGbf8yaB0FLzBUZC9RTAvc9KYGHXRd9eLHDBt28LRA7H74hRP0hIE5Pxpjw
	VdON2uSDktf0v8cCon1tJ0rfVS+5TlT3WGMsZs/FoIEXv+d9gAWYeyhYkYYdf/PH
	d0PWX6V6GSBZwUZ++1q12BxiPamDcn/zt90iJcP78CGDajVWIJ9fWdVNRLfxJXfF
	AKsHfilCsos9mh+AtFSiCLIf+bhPdwjYTgnd8nwwh1dsfxb1Cjwjjslg7Akuh7jj
	3bGf8I/0qUEQuyQAeJ0gZy+w92VjMkktykm13ZjkePcUnq0IH0Zf//0Iqr0IxuNh
	J4O8r7Pst8POfb3wUAopcqRA4N1298Js9EtQ7rMfaWviWmZGa6CMr23OMVJ+T9gZ
	93gghRXDdvlq676f/OuLEesf7XlEudKSrFh0P4GiUJ/CsbdaY0z4ptXlzy+hb9yX
	tJSOieZBNjOsCGybvETWvne2QQ7bjrQ2TWF0dGhpYXMgU2NoaWZmZXIgPHNjaGlm
	ZmVyQGluZm9ybWF0aWsudW5pLWx1ZWJlY2suZGU+iQIfBDABCgAJBQJWFXt3Ah0A
	AAoJEBbvP2TLIB2cXlQQAMnAo1aXy9DXx3Gz6IdHj4qd5op9WtkQmQYxkST+1imv
	yaVfZsON3f/+iVxYzUO1Gr69TY+1DRFEGFRccE1P4z0875Hji6SJhGZf5aZ06mrA
	6HMMMTKiQFIvL84FSBXRWTlIqNC6DJ9bXWEeqHA5d3gSqkrC2Y9DSKv53IXazGLu
	aoP0WHyPRpStc+TAlZyTbbfZSOL+1Uf8eAqkLV7No/SK88NTM/hQY9uieytHJGpO
	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
	frse+86sDR4=
	=wCzL
	-----END PGP PUBLIC KEY BLOCK-----
	EOF



::

	sudo apt-get install xinetd git vnstat vnstati gdebi-core lighttpd fastd build-essential \
	bridge-utils isc-dhcp-server radvd libnl-3-dev pkg-config apt-transport-https
	sudo apt-get update

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
* apt-transport-https wird zum Herunterladen von fastd benötigt


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
