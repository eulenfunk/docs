BGP Konzentrator einrichten
---------------------------

Der BGP Konzentrator ist der Backboneseitige unserer zwei Freifunk Server, er übernimmt Routing, NAT, Connection tracking, GRE Tunnel und BGP Sessions.

Für die virtuelle Maschine benötigen wir eine öffentliche IPv4 Adresse. Diese könnt ihr beim Rechenzentrum kaufen, nennt sich z.B. Failover IP. Für diese IP Adresse muss im Kundeninterface eine MAC Adresse erstellt werden, die dann im Proxmox auf der Netzwerkkarte der virtuellen Maschine konfiguriert wird.

Im Kundeninterface wird "IP" ausgewählt

.. image:: http://freifunk-mk.de/gfx/sys-1.png

In dem erscheinenden Formular klickt man das Zahnrad an der betreffenden IP-Adresse an und wählt "Eine virtuelle MAC-Adresse hinzufügen"

.. image:: http://freifunk-mk.de/gfx/sys-2.png

Im folgenden muss "Eine neue virtuelle MAC-Adresse erstellen" angeklickt werden und der Name der VM eingetragen werden.

.. image:: http://freifunk-mk.de/gfx/sys-3.png


Auf dem Webinterface des Proxmox Servers eine VM anlegen.

"Datacenter" -> "Servername" -> "Create VM"

.. image:: http://freifunk-mk.de/gfx/proxmox-6.png
----

Im Reiter 'General' eine Freie ID und einen Namen festlegen.

.. image:: http://freifunk-mk.de/gfx/proxmox-7.png
----

Im Reiter 'OS' 'Linux 4.x/3.x/2.6 Kernel auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-8.png
----

Im Reiter 'CD/DVD' das ISO Image auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-9.png
----

Im Reiter 'Hard Disk' als 'Bus' 'VirtIO' einstellen, die Festplattengröße auf 6GB begrenzen und als Format 'qcow2' wählen. Größere Festplatten machen Backups, Rollbacks und co nur aufwändiger.

.. image:: http://freifunk-mk.de/gfx/proxmox-10.png

Im Reiter 'CPU' ein Prozessorkern zuweisen. Als CPU kann man "host" wählen, das tut der Performance gut und HA nutzen wir ohnehin nicht.

.. image:: http://freifunk-mk.de/gfx/proxmox-11.png


Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 - 1024MB festlegen. Weniger als 256 hindert einige Maschinen beim booten, mehr als 1024 werden nicht benötigt.

.. image:: http://freifunk-mk.de/gfx/proxmox-12.png


Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diese VM zu verwendenden öffentlichen IPv4 Adresse eintragen. Bridged Mode übernehmen wir so und vmbr0 auch diese.

.. image:: http://freifunk-mk.de/gfx/vm_network.jpg


Bestätigen und Anlegen auswählen.

.. image:: http://freifunk-mk.de/gfx/vm_summary.jpg



Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden Verzögerung. Details lassen sich ausklappen.

Hinweis: Wenn das System später läuft, nicht vergessen, die Option "Start at boot" auf "Yes" zu stellen.

"Datacenter" -> "Servername" -> "Vmname" -> "Options" -> "Start at boot"

Und nach Installation das Iso aus dem lauffwerk nehmen, denn wenn die Datei irgendwann mal vom Storage gelöscht werden booten die Maschinen mangels ISO nicht mehr.

"Datacenter" -> "Servername" -> "Vmname" -> "Hardware" -> "CD/DVD Drive" -> "Do not use any media"

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

"Datacenter" -> "Servername" -> "Vmname" -> "Console" -> "Start"

Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

.. image:: http://freifunk-mk.de/gfx/proxmox-18.png

.. image:: http://freifunk-mk.de/gfx/proxmox-19.png

Als Installationssprache jetzt nochmal Deutsch auswählen,

.. image:: http://freifunk-mk.de/gfx/proxmox-20.png

die Auswahl trotz unvollständiger Unterstützung bestätigen,

.. image:: http://freifunk-mk.de/gfx/proxmox-21.png

den Standort auswählen (Deutschland),

.. image:: http://freifunk-mk.de/gfx/proxmox-22.png

das Tastaturmodell nicht automatisch erkennen lassen

.. image:: http://freifunk-mk.de/gfx/proxmox-23.png

Herkunftsland der Tastatur "Deutsch"

.. image:: http://freifunk-mk.de/gfx/proxmox-24.png

Tastaturbelegung "Deutsch"

.. image:: http://freifunk-mk.de/gfx/proxmox-25.png


Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und "Das Netzwerk unkonfiguriert belassen".

Der Rechnername ist frei wählbar

.. image:: http://freifunk-mk.de/gfx/proxmox-33.png

Und der Benutzer angelegt werden. Zunächst der volle Benutzername

.. image:: http://freifunk-mk.de/gfx/proxmox-35.png

und dann das gewünschte Login

.. image:: http://freifunk-mk.de/gfx/proxmox-36.png

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

.. image:: http://freifunk-mk.de/gfx/proxmox-37.png

Da auf dem Server keine persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png

Zeitzone Prüfen und bestätigen.

Festplatte manuell formatieren

.. image:: http://freifunk-mk.de/gfx/proxmox-39.png

Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-40.png

Partitionstabelle erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-41.png


Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-42.png
.. image:: http://freifunk-mk.de/gfx/proxmox-43.png


Partitionsgröße 5 GB Primär am Anfang

.. image:: http://freifunk-mk.de/gfx/proxmox-44.png
.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
.. image:: http://freifunk-mk.de/gfx/proxmox-46.png


Bootflag auf 'ein' setzen und 'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-47.png


Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-48.png


Eine neue Partition erstellen

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


"OpenSSH" server auswählen (Leertaste benutzen) und weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-56.png


Warten...

Die Installation des GRUB Bootloader bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-57.png


Weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-58.png


Nach dem Reboot auf der Proxmox Konsole am Server anmelden und die Netzwerkkonfiguration erstellen.

Zuerst muss der Name der Netzwerkkarte ermittelt werden.

::

	ip l

Dort sind zwei Netzwerkkarten aufgelistet einmal "lo:" und einmal z.B. "ens18", letztere muss konfiguriert werden.

In der /etc/network/interfaces müssen IP Adresse, Netzmaske, Gateway, DNS Server und Routen konfiguriert werden.

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

Den nachfolgenden ssh Kommandos muss man die Option "-p 45926" (kleines "p"!) und den scp Kommandos
die Option "-P 45926" (großes "P"!).

::

			ssh -p 45926 meinbenutzername@111.222.333.444


Systemaktualisierung
^^^^^^^^^^^^^^^^^^^^

Als Nächstes steht die Systemaktualisierung an; auch hier beim erstmaligen Aufruf die Nutzung von IPv4 erzwingen für's APT-Get

::

	sudo apt update
	sudo apt dist-upgrade
	sudo apt autoremove


Unnötige Pakete deinstallieren und unötige Dienste deaktivieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Standardmäßig werden von Canonical Pakete installiert und Dienste gestartet, die man auf den meisten Servern
nicht benötigt. Wir räumen deshalb auf und deinstallieren Pakete:

::
	sudo apt remove lxcfs snapd

Danach werden die unnötigen Dienste noch disabled:

::

	sudo systemctl disable mdadm
	sudo systemctl disable iscsid
	sudo systemctl disable lvm2-lvmetad


Pakete installieren
^^^^^^^^^^^^^^^^^^^

::

	sudo apt install htop iftop bird xinetd vnstat gdebi-core conntrack speedtest-cli

* bird übernimmt das BGP routing
* vnstat monitort den Netzwerktraffic
* gdebi-core ermöglicht uns die Installation des Check_mk Agents
* xinetd ist der bei Debian übliche Super-Daemon, über ihn wird der Check_mk Agent angesprochen
* conntrack überwacht den Auslastungszustand der NAT-Engine
* htop für das Monitoren der Prozesse
* iftop für das Monitoren des Netzwerktraffics
* speedtest-cli bietet eine Möglichkeit Netzwerkdurchsatz zu testen


Hinzufügen einer weiteren Netzwerkschnittstelle ens19
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Für die Verbindung zwischen den Supernodes und dem Konzentrator legen wir eine zweite Netzwerkschnittstelle an.
Dazu muss im Proxmox für die VM eine Netzwerkkarte hinzugefügt werden, die auf der vmbr1 hängt und virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die VM einmal herunterfahren und erneut starten. Ein Reboot reicht hier nicht!

GRE Tunnel zum Freifunk Rheinland Backbone einrichten
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Da wir unsere Freifunk Domäne über das Freifunk Rheinland Backbone an das Internet anbinden wollen müssen wir zuerst eine virtuelle Kabelverbindung herstellen in Form von GRE Tunneln.

Dazu legen wir pro Backbone Standort einen Tunnel an, der zur IP des Standortes verbunden wird und intern je Ende eine Tunnelip hat.

Aktuell gibt es 6 Backbone Standorte:

* Berlin A + B
* Düsseldorf + B
* Frankfurt A + B

Die IPs für die Tunnel bekommt ihr vom Freifunk Rheinland Backbone Team.

Die Tunnelkonfiguration wird in die :code:`/etc/network/interfaces` eingetragen.

* address -> lokale IP im Tunnel
* dstaddr -> entfernte IP im Tunnel (Freifunk Rheinland Seite)
* endpoint -> Der Backbone Standort zu dem der Tunnel aufgebaut wird
* local -> die eigene IPv4 Adresse des Servers (FailoverIP)
* per :code:`post-up` wird dem Tunnel die lokale IPv6 Adresse im Tunnel zugewiesen

::

	auto  tun-ffrl-ber-a
	iface tun-ffrl-ber-a inet tunnel
        mode            gre
        address         100.xx.x.xx
        dstaddr         100.yy.y.yy
		netmask         255.255.255.254
		local           111.222.333.444
        endpoint        185.66.195.0
        ttl             255
        mtu             1400
        post-up ip -6 addr add 2a03:2260:z:zzz::2/64 dev $IFACE


Dieser Block muss für alle 6 Standorte angelegt werden, wobei "tun-ffrl-ber-a" dann angepasst werden muss.

Da wir die Daten nicht über unsere Failover IP ins Internet schicken haben wir vom Freifunk Rheinland eine FFRL-exit-IP zugewiesen bekommen, bzw. oft ein kleines Netz, wie z.B. 185.66.195.ww/31

Diese muss auch als virtuelles Interface in der Netzwerkkonfiguration angelegt werden.

::

	auto tun-ffrl-uplink
	iface tun-ffrl-uplink inet static
        address 185.66.195.ww
        netmask 255.255.255.255
        pre-up ip link add $IFACE type dummy
        post-down ip link del $IFACE

Nun wird der Server einmal neu gestartet.

Nach dem Neustart sollten die Tunnel alle bei einem "ip a" angezeigt werden.

Zum Testen ob alle Tunnel funktionieren sollten wir jeweils einmal einen ping auf die IPv4 dstaddr machen:

::

	ping 100.yy.y.yy


Und für IPv6 einen Ping auf die IPv6 Adresse, wobei die "2" (lokal) am Ende durch eine "1" (FFRL Seite) ersetzt werden muss,

::

	ping6 2a03:2260:z:zzz::1


BGP Einrichten
^^^^^^^^^^^^^^

Um dynamisch Routen vom FFRL zu bekommen und auch Routen in unsere Netze zu propagieren, nutzen wir das BorderGatewayProtokol kurz BGP. Hierfür nutzen wir Bird.

Die Bird Config liegt unter :code:`/etc/bird/bird.conf`.

Hinweis: in diesen Ordner kommt man nicht ohne Root-Rechte, muss man aber auch nicht.

Als erstes der IPv4 Teil:

::

	sudo nano /etc/bird/bird.conf


::

	# Die FFRL Exit IP als BGP Router ID
	router id 185.66.195.ww;

		protocol direct announce {
			table master;
			import where net ~ [185.66.195.ww/32];
			interface "tun-ffrl-uplink";
		};

		protocol kernel {
			table master;
			device routes;
			import none;
			export filter {
				# FFRL Exit IP
				krt_prefsrc = 185.66.195.ww;
				accept;
			};
			# Die Routingtabelle in die die gelernten Routen durch bird automatisch eingetragen werden
			kernel table 42;
		};

		protocol device {
			scan time 15;
		};

		function is_default() {
			return (net ~ [0.0.0.0/0]);
		};

		# Template wird bei jeder BGP Session eingebunden, sodass man die Werte nicht überall einzeln angeben muss
		template bgp uplink {
			# Eigene private AS Nummer (vom FFRL zugewiesen)
			local as 65vvv;
			import where is_default();
			export where proto = "announce";
		};

		# BGP Session mit dem Backbone Standort Berlin A
		protocol bgp ffrl_ber_a from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};
		# BGP Session mit dem Backbone Standort Berlin B
		protocol bgp ffrl_ber_b from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};
		# BGP Session mit dem Backbone Standort Düsseldorf A
		protocol bgp ffrl_dus_a from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};
		# BGP Session mit dem Backbone Standort Düsseldorf B
		protocol bgp ffrl_dus_b from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};
		# BGP Session mit dem Backbone Standort Frankfurt A
		protocol bgp ffrl_fra_a from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};
		# BGP Session mit dem Backbone Standort Frankfurt B
		protocol bgp ffrl_fra_b from uplink {
			source address 100.xx.x.xx;
			neighbor 100.yy.y.yy as 201701;
		};

		# AS201701 ist das AS des Freifunk Rheinland

Bis hierhin testen wir schonmal:

::

	sudo systemctl start bird
	sudo birdc s p

Hierbei sollte Output ähnlich dem folgenden ausgegegen werden.
Der State sollte auf 'up' und die Info auf 'Established' sein.
Es kann 3 Minuten dauern bis alle Sessions stehen:

::

	BIRD 1.5.0 ready.
	name     proto    table    state  since       info
	announce Direct   master   up     19:41:11
	kernel1  Kernel   master   up     19:41:11
	device1  Device   master   up     19:41:11
	ffrl_ber_a BGP      master   up     19:41:13    Established
	ffrl_dus_a BGP      master   up     19:41:15    Established
	ffrl_ber_b BGP      master   up     19:41:13    Established
	ffrl_dus_b BGP      master   up     19:41:15    Established


Als nächstes nehmen wir und den IPv6 Teil vor:

::

	sudo nano /etc/bird/bird6.conf


::

	# Die FFRL Exit IP als BGP Router ID
	router id 185.66.195.ww;

		protocol kernel {
			device routes;
			import none;
			export all
			# Die Routingtabelle in die die gelernten Routen durch bird automatisch eingetragen werden
			kernel table 42;
		};

		protocol device {
			scan time 10;
		};

		function is_default() {
			return (net ~ [::/0]);
		};

		# Nur /56er Netze aus dem zugewiesenen /48er Netz werden exportiert
		filter hostroute {
			if net ~ [2a03:2260:xxx::/48{56,56}] then accept;
			reject;
		}

		# Template wird bei jeder BGP Session eingebunden, sodass man die Werte nicht überall einzeln angeben muss
		template bgp uplink {
			#Eigene private AS Nummer (vom FFRL zugewiesen)
			local as 65vvv;
			import where is_default();
			export filter hostroute;
			gateway recursive;
		};

		# BGP Session mit dem Backbone Standort Berlin A
		protocol bgp ffrl_ber_a from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		# BGP Session mit dem Backbone Standort Berlin B
		protocol bgp ffrl_ber_B from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		# BGP Session mit dem Backbone Standort Düsseldorf A
		protocol bgp ffrl_dus_a from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		# BGP Session mit dem Backbone Standort Düsseldorf B
		protocol bgp ffrl_dus_B from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		# BGP Session mit dem Backbone Standort Frankfurt A
		protocol bgp ffrl_fra_a from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		# BGP Session mit dem Backbone Standort Frankfurt B
		protocol bgp ffrl_fra_B from uplink {
			source address 2a03:2260:0:nnn::2;
			neighbor 2a03:2260:0:nnn::2; as 201701;
		};
		#AS201701 ist das AS des Freifunk Rheinland

Den IPv6 Teil testen wir auch wieder:

::

	sudo birdc6 s p

Der Output sollte so ähnlich aussehen wie unten, auch hier muss der State wieder "up" und die
Info "Established" sein:

::

	BIRD 1.5.0 ready.
	name     proto    table    state  since       info
	announce Direct   master   up     19:41:11
	kernel1  Kernel   master   up     19:41:11
	device1  Device   master   up     19:41:11
	ffrl_ber_a BGP      master   up     19:41:13    Established
	ffrl_dus_a BGP      master   up     19:41:15    Established
	ffrl_ber_b BGP      master   up     19:41:13    Established
	ffrl_dus_b BGP      master   up     19:41:15    Established


Wenn bis hierher alles geklappt hat, stellen wir sicher, dass :code:`bird` und :code:`bird6` nach einem
Reboot automatisch gestartet werden:

::

	sudo systemctl enable bird
	sudo systemctl enable bird6


Die von Bird gesetzte Defaultroute muss nun in der Routingtabelle 42 erscheinen:

::

	ip r s t 42

::

	default via 100.64.y.yyy dev tun-ffrl-dus-a  proto bird  src 185.66.195.ww

::

	ip -6 r s t 42

::

	default via 2a03:2260:0:nnn::1 dev tun-ffrl-dus-a  proto bird  metric 1024


Die zweite Netzwerkschnittstelle konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Wir verwenden das Netz 172.31.0.0/24 für die Kommunikation zwischen Konzentrator und den Supernodes

::

	sudo nano /etc/network/interfaces

::

	auto ens19
	iface ens19 inet static
		address 172.31.254.254
		netmask 255.255.255.0


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

	# Das Conntracking sorgt beim NAT dafür dass die Antwortpakete an den ursprünglichen Client zugestellt werden können. Jede Anfrage wird in einer Tabelle vorgehalten. Ist diese voll läuft nichts mehr. Daher setzen wir ein großes Tabellenmaximum
	net.netfilter.nf_conntrack_max=1337000
	# Normalerweise werden nur Pakete akzeptiert, für die auf dem selben Interface auch eine Anfrage gesendet wurde. Aufgrund des Asymmetrischen Routings kommen Antwortpakete nicht immer auf dem selben ffrl-tun Interface an, auf dem die Anfrage gesendet wurde. Folgende Parameter ermöglichen den Paketempfang trotz des Asymmetrischen routings.
	net.ipv4.conf.default.rp_filter=2
	net.ipv4.conf.all.rp_filter=2


Wieder einmal das Systen rebooten und danach noch einmal GRE, BGP, BGP6 und ens19 prüfen.

Zur Erinnerung wir haben ja nur eine öffentliche IPv4 Adresse vom FFRL bekommen und möchten viele hundert Endgeräte ins Netz bringen, die alle nur private IPv4 Adressen bekommen.
Daher nutzen wir Network-Address-Translation -> NAT.
Die Einrichtung passiert über :code:`ferm`.
Hinweis: die folgenden Schritte müssen alle abgeschlossen werden bevor ein Reboot erfolgen kann, ansonsten ist ein Zugriff auf das System unter Umständen nur noch über den Hypervisor möglich.

Ferm installieren

::

	sudo apt install ferm

::

	sudo nano /etc/ferm/ferm.conf

::

	domain (ip ip6) {
	    table filter {
			chain INPUT {
		    	policy ACCEPT;
		    	proto gre ACCEPT;
		    	mod state state INVALID DROP;
		    	mod state state (ESTABLISHED RELATED) ACCEPT;
		    	interface lo ACCEPT;
		    	proto icmp ACCEPT;
		    	proto udp dport 500 ACCEPT;
		    	proto (esp) ACCEPT;
		    	# SSH Zugriff mit dem richtigen Port hier erlauben!
		    	proto tcp dport 45926 ACCEPT;
			}
			chain OUTPUT {
		    	policy ACCEPT;
		    	mod state state (ESTABLISHED RELATED) ACCEPT;
			}
			chain FORWARD {
		    	policy ACCEPT;
		    	mod state state INVALID DROP;
		    	mod state state (ESTABLISHED RELATED) ACCEPT;
			}
		}
		table mangle {
			# Pakete die von einem der ffrl-tunnelinterfaces kommen mit einem fw-mark versehen. Dies wird später benötigt um die Pakete in die richtige Routingtabelle zu leiten.
			chain PREROUTING {
		    	interface tun-ffrl-+ {
					MARK set-mark 1;
		    	}
			}
			# Aus Gründen(TM) müssen wir die Paketgröße anfassen damit die Päckchen vor lauter Headerfoo überhaupt noch irgendwo durchkommen.
			chain POSTROUTING {
		    	outerface tun-ffrl-+ proto tcp tcp-flags (SYN RST) SYN TCPMSS clamp-mss-to-pmtu;
			}
		}
		table nat {
			# Hier findet das Nat zwischen privatem Netzbereich und FFRL-Exit-IP statt
			chain POSTROUTING {
		    	outerface tun-ffrl-+ saddr 172.16.0.0/12 SNAT to 185.66.195.xx;
		    	policy ACCEPT;
			}
		}
	}


Hier einen Reboot und danach prüfen ob man noch ins System kommt.
Wenn ja -> weiter machen.
Wenn nein -> per Proxmox drauf zugreifen und richtig konfigurieren.

Die Pakete die von den verschiedenen Interfaces kommen müssen in die richtigen Routingtabellen geschickt werden

::

	sudo nano /etc/rc.local

::

	# Alle Pakete mit FW Mark -> Tabelle 42
	ip -4 rule add prio 1000 fwmark 0x1 table 42
	ip -6 rule add prio 1000 fwmark 0x1 table 42

	# Alle Pakete von FFRL Tunneln -> Tabelle 42
	ip -4 rule add prio 1001 iif ffrl-tun-ber-a table 42
	ip -4 rule add prio 1001 iif ffrl-tun-ber-b table 42
	ip -4 rule add prio 1001 iif ffrl-tun-dus-a table 42
	ip -4 rule add prio 1001 iif ffrl-tun-dus-b table 42
	ip -4 rule add prio 1001 iif ffrl-tun-fra-a table 42
	ip -4 rule add prio 1001 iif ffrl-tun-fra-b table 42
	ip -6 rule add prio 1001 iif ffrl-tun-ber-a table 42
	ip -6 rule add prio 1001 iif ffrl-tun-ber-b table 42
	ip -6 rule add prio 1001 iif ffrl-tun-dus-a table 42
	ip -6 rule add prio 1001 iif ffrl-tun-dus-b table 42
	ip -6 rule add prio 1001 iif ffrl-tun-fra-a table 42
	ip -6 rule add prio 1001 iif ffrl-tun-fra-b table 42



Monitoring
^^^^^^^^^^

Das Monitoring beinhaltet folgende Komponenten:

* Check_MK ermöglicht das zentrale Monitoring aller Systemdaten aller eingebundenen Server
* vnstat erstellt Traffic Statistiken, die sich auf der shell anzeigen lassen

Check_MK Agent installieren
...........................

Den Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit:

In die CheckMK-Instanz per Webbrowser einloggen. Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.4.0p8-1_all.deb _(Beispiel)_

Den Download-Link in die Zwischenablage kopieren.
Im SSH-Terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget https://monitoring.eulenfunk.de/eulenfunk/check_mk/agents/check-mk-agent_1.4.0p8-1_all.deb

Um das .deb Paket zu installieren wird :code:`gdebi` empfohlen, ausserdem benötigt der Agent :code:`xinetd` zum Ausliefern der Monitoring Daten.

Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	sudo gdebi check-mk-agent_1.4.0p8-1_all.deb

Anschließend noch das Konzentrator-Plugin hinzufügen:

::

	cd /usr/lib/check_mk_agent/local
	sudo wget -O konzentrator https://raw.githubusercontent.com/eulenfunk/check_mk/master/konzentrator
	sudo chmod 755 konzentrator
	sudo chmod +x konzentrator

::
		sudo nano /etc/xinetd.d/check_mk

Dort die Zeile

::

	# only_from = 127.0.0.1 10.0.20.1 10.0.20.2

ändern in

::

		only_from = 127.0.0.1 xx.yy.ab.cd

Hierbei muss :code:`xx.yy.ab.cd` durch die IP-Adresse des Check_MK Servers ersetzt
werden.

Damit diese Änderungen aktiviert werden, muss der xinetd durchgestartet werden

::

	sudo systemctl  restart xinetd


Der Rechner hält ab nun Daten zum Abruf bereit.
