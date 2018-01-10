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

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und "Netzwerk unkonfiguriert lassen" auswählen.

Der Rechnername ist frei wählbar z.b. meinestadt-1

.. image:: http://freifunk-mk.de/gfx/proxmox-33.png

Und der Benutzername.

.. image:: http://freifunk-mk.de/gfx/proxmox-35.png

.. image:: http://freifunk-mk.de/gfx/proxmox-36.png

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

.. image:: http://freifunk-mk.de/gfx/proxmox-37.png

Da auf dem Server keine Persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png

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

Netzwerkschnittstelle konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nach dem Reboot auf der Proxmox Konsole am Server anmelden und die Netzwerkkonfiguration erstellen.

Zuerst muss der Name der Netzwerkkarte ermittelt werden.

::

	ip l

Dort sind zwei Netzwerkkarten aufgelistet einmal :code:`lo:` und einmal z.B. :code:`ens18`,
letztere muss konfiguriert werden.

In der :code:`/etc/network/interfaces` müssen IP Adresse, Netzmaske, Gateway, DNS Server und Routen konfiguriert werden.

Die Gatewayadresse ist bei OVH/SYS Servern die Adresse des Blechs, wobei der letzte Block durch 254 ersetzt wird.

Hat das Blech also die IP 555.666.777.888 ist die Gatewayadresse 555.666.777.254

::

	sudo nano /etc/network/interfaces


::

	auto lo
	iface lo inet loopback

	auto ens18
	iface ens18 inet static
	address 111.222.333.444
	netmask 255.255.255.255
	dns-nameservers 8.8.8.8
	post-up ip r add 555.666.777.254 dev ens18
	post-up ip r add default via 555.666.777.254
	post-down ip r del default via 555.666.777.254
	post-down ip r del 555.666.777.254 dev ens18

Nun erfolgt ein Neustart der Maschine mit

::

	sudo reboot


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

Nun das Password-Login auf dem Server deaktivieren. Dazu die :code:`sshd_config` editieren:

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

	Port 45926

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

	sudo systemctl restart ssh

Den nachfolgenden :code:`ssh` Kommandos muss man die Option :code:`-p 45926` (kleines "p"!) und den :code:`scp` Kommandos
die Option :code:`-P 45926' (großes "P"!).

::

			ssh -p 45926 meinbenutzername@111.222.333.444


Unnötige Pakete deinstallieren und unötige Dienste deaktivieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Standardmäßig werden von Canonical Pakete installiert und Dienste gestartet, die man auf den meisten Servern
nicht benötigt. Wir räumen deshalb auf und deinstallieren Pakete:

::
	sudo apt remove lxcfs snapd

Danach werden die unnötigen Dienste noch deaktiviert:

::

	sudo systemctl disable mdadm iscsid lvm2-lvmetad

Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als Nächstes steht die Systemaktualisierung an; auch hier beim erstmaligen Aufruf die Nutzung von IPv4 erzwingen für's APT-Get

::

	sudo apt update
	sudo apt dist-upgrade
	sudo apt autoremove

Pakete installieren
^^^^^^^^^^^^^^^^^^^

::

	sudo apt install htop iftop xinetd git vnstat gdebi-core build-essential \
		bridge-utils isc-dhcp-server radvd cmake doxygen bison pkg-config \
		libjson0 libjson0-dev libcap-dev  libnl-3-dev libnl-genl-3-dev

Rückfrage mit "j" bestätigen

Um welche Paket handelt es sich?

* vnstat monitort den Netzwerktraffic
* gdebi-core ermöglicht uns die Installation des Check_mk Agents
* xinetd ist der bei Debian übliche Super-Daemon, über ihn wird der Check_mk Agent angesprochen
* build-essential wird zum kompilieren von Batman benötigt
* bridge-utils (brctl) steuert Netzwerkbrücken
* isc-dhcp-server (dhcpd3) verteilt IPv4 Adressen
* radvd verteilt die IPv6 Range
* git wird für die Konfigurationsscripte benötigt
* libnl-3-dev wird für batman benötigt
* pkg-config wird für batctl benötigt
* htop für das Monitoren der Prozesse
* iftop für das Monitoren des Netzwerktraffics
* speedtest-cli bietet eine Möglichkeit Netzwerkdurchsatz zu testen

Libuecc kompilieren
^^^^^^^^^^^^^^^^^^^

::

	git clone http://git.universe-factory.net/libuecc
	cd libuecc
	cmake ./
	make
	sudo make install
	sudo ldconfig


Libsodium kompilieren
^^^^^^^^^^^^^^^^^^^^^

::

	wget https://download.libsodium.org/libsodium/releases/libsodium-1.0.12.tar.gz
	tar -xzf libsodium-1.0.12.tar.gz
	cd libsodium-1.0.12/
	./configure
	make && make check
	sudo make install

Fastd kompilieren
^^^^^^^^^^^^^^^^^

::

	git clone git://git.universe-factory.net/fastd
	cd fastd
	cmake ./ -DCMAKE_BUILD_TYPE=RELEASE
	make
	sudo make install


Batman kompilieren
^^^^^^^^^^^^^^^^^^

Batman kann man bei http://www.open-mesh.org/projects/open-mesh/wiki/Download herunterladen

::

	cd ~
	wget http://downloads.open-mesh.org/batman/stable/sources/batman-adv/batman-adv-2017.3.tar.gz
	tar -xf batman-adv-2017.3.tar.gz
	cd batman-adv-2017.3
	make
	sudo make install


Batctl kompilieren
^^^^^^^^^^^^^^^^^^

::

	cd ~
	sudo wget https://downloads.open-mesh.org/batman/stable/sources/batctl/batctl-2017.3.tar.gz
	tar -xf batctl-2017.3.tar.gz
	cd batctl-2017.3
	make
	sudo make install

Batman Kernelmodul eintragen
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Damit das Batman Kernelmodul beim Boot geladen, wird müssen wir es noch in die :code:`/etc/modules` eintragen.

Mehr Infos gibt es im Ubuntuusers wiki https://wiki.ubuntuusers.de/Kernelmodule#start

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
	#status socket "/run/fastd.client.sock";

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

	sudo su
	fastd --generate-key > secret.conf
	exit

In der Datei secret.conf müssen dann manuell Änderungen vorgenommen werden:
Die Zeile mit 'Public' muss mit '#' auskommentiert werden, die Zeile 'Secret' muss angepasst werden.

::

	sudo nano secret.conf

::

	secret "xxx...";
	#Public: ...

Sysctl Parameter setzen
^^^^^^^^^^^^^^^^^^^^^^^
Es müssen einige Systemparameter die das Networking betreffen per :code:`sysctl` gesetzt werden:

::

	sudo nano /etc/sysctl.d/20-freifunk.conf

::

	# Dem System erlauben Pakete zwischen einzelnen Netzwerkinterfaces hin und her zu routen
	net.ipv4.ip_forward=1
	net.ipv6.conf.all.forwarding=1

	# Mehr Netzwerkdurchsatz
	net.ipv4.tcp_window_scaling = 1
	net.core.rmem_max = 16777216
	net.ipv4.tcp_rmem = 4096 87380 16777216
	net.ipv4.tcp_wmem = 4096 16384 16777216


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

	cd ~
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


Hinzufügen einer Schnittstelle ens19
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Nun muss im Proxmox für die VM eine ens19 hinzugefügt werden, die auf der vmbr1 hängt und Virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die VM einmal durchbooten.

::
	sudo nano /etc/network/interfaces

::
	(...)
	auto ens19
	iface ens19 inet static
		address 172.31.254.1
		netmask	255.255.255.0
		post-up ip -6 2a03:2260:xx:xx::2/56 dev ens19


Zusätzlich muss eine Bridge :code:`br0` in der :code:`/etc/network/interfaces`
angelegt werden:

::

	(...)
	auto br0
	iface br0 inet static
		address 172.xx.0.1
		netmask 255.255.0.0
		bridge_ports none
		bridge_stp no
		post-up ip -6 addr add 2a03:2260:yyy:zzz::3/64 dev br0

DHCP-Server konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^

::
	sudo nano /etc/dhcp/dhcpd.conf

::

	authoritative;
	subnet 172.19.0.0 netmask 255.255.0.0 {
        range 172.xx.1.1 172.xx.250.254;
        default-lease-time 3600;
        max-lease-time 86400;
        option domain-name-servers 8.8.8.8;
        option routers 172.xx.0.1;
        #option interface-mtu 1372;
        option interface-mtu 1280;
        interface br0;
	}
	# Statische Zuordnungen
	host Beispielhost { fixed-address 172.xx.251.1; hardware ethernet yy:yy:yy:yy:yy:yy; }


Dann den DHCP-Server für den automatischen Start vorbereiten und starten:

::

	sudo systemctl enable isc-dhcp-server
	sudo systemctl start isc-dhcp-server

RADVD einrichten
^^^^^^^^^^^^^^^^

::

	sudo nano /etc/radvd.conf

::

	interface br0 {
		AdvSendAdvert on;
		MaxRtrAdvInterval 600;
		MinDelayBetweenRAs 10;
		AdvLinkMTU 1280;
		prefix 2a03:2260:yyy:zzz::/64 {
			AdvRouterAddr on;
  		};
  		RDNSS 2620:0:ccc::2 2001:4860:4860::8888 {
  		};
	};

Den Dienst aktivieren und starten:

::

	sudo systemctl enable radvd
	sudo systemctl start radvd





Verbindung zwischen Supernode und Konzentrator konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Auf dem Supernode
.................

::

	sudo nano /etc/rc.local

::

	# Für IPv4
	# Tabelle 42 mit  einer Route je Richtung befüllen
	ip r add t 42 default via 172.31.254.254 dev ens19
	ip r add t 42 172.19.0.0/16 dev br0

	# Regeln anlegen, damit Pakete durch Tabelle 42 geroutet werden
	ip rule add prio 1000 from 172.19.0.0/16 lookup 42
	ip rule add prio 1001 from all iif ens19 lookup 42
	ip rule add prio 2000 from 172.19.0.0/16 type unreachable

	# Für IPv6
	# Tabelle 42 mit  einer Route je Richtung befüllen
	ip -6 r add t 42 2a03:2260:120:300::/64 dev br0
	ip -6 r add t 42 2a03:2260:120:300::1 dev ens19
	ip -6 r add t 42 default via 2a03:2260:120:300::1

	# Regeln anlegen, damit Pakete durch Tabelle 42 geroutet werden
	ip -6 rule add prio 1000 from 2a03:2260:120:300::/56 lookup 42
	ip -6 rule add prio 1001 from all iif ens19 lookup 42
	ip -6 rule add prio 2000 from 2a03:2260:120:300::/56 type unreachable

	# IPTables Regeln
	iptables -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1200
	ip6tables -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1200


####DEV17 ab hier TODO

Danach den Supernode rebooten.

Hier eine grafische Übersicht über die beteiligten Konfigurationsdateien auf dem Supernode:

.. image:: https://raw.githubusercontent.com/eulenfunk/supernode/master/Supernode-Routing.png


Auf dem Konzentrator
....................

Auf dem Konzentrator muss die zum Supernode passende Konfiguration angelegt werden:

::

	sudo nano /etc/rc.local

::

	(...)
	# Ab hier müssen die Einträge für jeden Supernode wiederholt werden!
	# Alle Pakete vom ersten Supernode -> Tabelle 42
	ip -4 rule add prio 1000 from 172.xx.0.0/16 table 42
	ip -6 rule add prio 1000 from 2a03:2260:yyy:zzz::/56 table 42

	# Unreachable default route, damit Freifunk Pakete nie über die ens18 default route g$
	ip -4 rule add prio 2000 from 172.xx.0.0/16 type unreachable
	ip -6 rule add prio 2000 from 2a03:2260:yyy:zzz::/56 type unreachable

	# Pakete, die vom FFRL Tunnel in die Tabelle 42 kommen müssen von dort über die ens19$
	ip -4 route add 172.xx.0.0/16 via 172.31.254.xx dev ens19 table 42
	ip -6 route add 2a03:2260:yyy:zzz::/64 via 2a03:2260:yyy:zzz::2 table 42
