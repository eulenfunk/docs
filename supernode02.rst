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


Auf dem Webinterface des Proxmox Servers ist auf der linken Seite das Blech auszuwählen und dann oben rechts 'Create VM' anklicken

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
----

Im Reiter 'CPU' ein Prozessorkern zuweisen. Als CPU kann man "host" wählen, das tut der Performance gut und HA nutzen wir ohnehin nicht.

.. image:: http://freifunk-mk.de/gfx/proxmox-11.png
----

Im Reiter 'Memory' unter 'Automatically allocate memory within this range' 256 - 1024MB festlegen. Weniger als 256 hindert einige Maschinen beim booten, mehr als 1024 werden nicht benötigt.

.. image:: http://freifunk-mk.de/gfx/proxmox-12.png
----

Im Reiter 'Network' als Netzwerkkarte 'VirtIO' auswählen und die MAC Adresse der für diese VM zu verwendenden öffentlichen IPv4 Adresse eintragen. Bridged Mode übernehmen wir so und vmbr0 auch diese.

.. image:: http://freifunk-mk.de/gfx/proxmox-13.png
----

Bestätigen und Anlegen auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-14.png

----

Fehlermeldungen während der Startphase werden unten im Log-Fenster angezeigt, erscheinen immer "oben", jedoch mit einigen Sekunden Verzögerung. Details lassen sich ausklappen.

Hinweis: Wenn das System später läuft, nicht vergessen, die Option "Start at boot" auf "Yes" zu stellen.

.. image:: http://freifunk-mk.de/gfx/proxmox-16.png
----
Und nach Installation das Iso aus dem lauffwerk nehmen, denn wenn die Datei irgendwann mal vom Storage gelöscht werden booten die Maschinen mangels ISO nicht mehr.

Ubuntu Server Installieren
^^^^^^^^^^^^^^^^^^^^^^^^^^

Die VM links auswählen und oben rechts starten und die Konsole öffnen

.. image:: http://freifunk-mk.de/gfx/proxmox-17.png
----

Deutsch als Sprache auswählen und nun Ubuntu Server Installieren

.. image:: http://freifunk-mk.de/gfx/proxmox-18.png

.. image:: http://freifunk-mk.de/gfx/proxmox-19.png
----

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
----

Sobald der Server versucht das Netzwerk automatisch zu konfigurieren, dies abbrechen und die manuelle Netzwerkkonfiguration auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-26.png

.. image:: http://freifunk-mk.de/gfx/proxmox-27.png

.. image:: http://freifunk-mk.de/gfx/proxmox-28.png
----

Die Failover-IP, für die wir vorhin die MAC-Adresse erstellt haben ist beispielsweise die 555.666.777.888

.. image:: http://freifunk-mk.de/gfx/proxmox-29.png
----

Die Subnetzmaske von 255.255.255.0 bleibt in der Regel so

.. image:: http://freifunk-mk.de/gfx/proxmox-30.png
----

Die Gateway Adresse sollte man beim Rechenzentrum erfragen.

Bei OVH/Soyoustart ist das IPv4 Gateway immer auf der 254, also 555.666.777.254

.. image:: http://freifunk-mk.de/gfx/proxmox-31.png
----

Als DNS geht z.B. der 8.8.8.8 von Google (Böse!).

.. image:: http://freifunk-mk.de/gfx/proxmox-32.png
----

Der Rechnername ist frei wählbar

.. image:: http://freifunk-mk.de/gfx/proxmox-33.png
----

Der Domainname ist hier einzutragen

.. image:: http://freifunk-mk.de/gfx/proxmox-34.png
----

Und der Benutzer angelegt werden. Zunächst der volle Benutzername

.. image:: http://freifunk-mk.de/gfx/proxmox-35.png

und dann das gewünschte Login

.. image:: http://freifunk-mk.de/gfx/proxmox-36.png
----

Das Kennwort sollte sicher sein und nicht bereits für einen anderen Zweck in Verwendung.

.. image:: http://freifunk-mk.de/gfx/proxmox-37.png
----

Da auf dem Server keine persönlichen Dateien gespeichert werden sollen ist es nicht notwendig den persönlichen Ordner zu verschlüsseln.

.. image:: http://freifunk-mk.de/gfx/proxmox-38.png
----

Zeitzone Prüfen und bestätigen.

Festplatte manuell formatieren

.. image:: http://freifunk-mk.de/gfx/proxmox-39.png
----

Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-40.png
----

Partitionstabelle erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-41.png
----

Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-42.png
.. image:: http://freifunk-mk.de/gfx/proxmox-43.png
----

Partitionsgröße 5 GB Primär am Anfang

.. image:: http://freifunk-mk.de/gfx/proxmox-44.png
.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
.. image:: http://freifunk-mk.de/gfx/proxmox-46.png
----

Bootflag auf 'ein' setzen und 'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-47.png
----

Freien Speicherplatz auswählen und enter

.. image:: http://freifunk-mk.de/gfx/proxmox-48.png
----

Eine neue Partition erstellen

.. image:: http://freifunk-mk.de/gfx/proxmox-49.png
----

Größe bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-50.png
----

Primär

.. image:: http://freifunk-mk.de/gfx/proxmox-45.png
----

Benutzen als 'Auslagerungsspeicher (SWAP)'

'Anlegen beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-51.png
----

'Partitionierung beenden'

.. image:: http://freifunk-mk.de/gfx/proxmox-52.png
----

Ja schreiben, noch sind ja keine Daten vorhanden, die überschrieben werden könnten.

.. image:: http://freifunk-mk.de/gfx/proxmox-53.png
----

Warten...

Proxy leer lassen

.. image:: http://freifunk-mk.de/gfx/proxmox-54.png
----

Warten...

Automatische Sicherheitsaktualisierungen auswählen

.. image:: http://freifunk-mk.de/gfx/proxmox-55.png
----

OpenSSH server auswählen (Leertaste benutzen) und weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-56.png
----

Warten...

Die Installation des GRUB Bootloader bestätigen

.. image:: http://freifunk-mk.de/gfx/proxmox-57.png
----

Weiter

.. image:: http://freifunk-mk.de/gfx/proxmox-58.png
----

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

::

	sudo apt-get install bird bird6 xinetd vnstat vnstati gdebi-core lighttpd git conntrack

* bird übernimmt das BGP routing
* bird6 tut das selbe für IPv6
* vnstat monitort den Netzwerktraffic
* vnstati erzeugt daraus Grafiken
* lighttpd stellt diese zum Abruf bereit
* gdebi-core ermöglicht uns die Installation des Check_mk Agents
* git wird für die Konfigurationsscripte benötigt
* xinetd ist der bei Debian übliche Super-Daemon, über ihn wird der Check_mk Agent angesprochen
* conntrack überwacht den Auslastungszustand der NAT-Engine

Hinzufügen einer Schnittstelle eth1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Für die Verbindung zwischen den Supernodes und dem Konzentrator legen wir eine zweite Netzwerkschnittstelle an.
Dazu muss im Proxmox für die VM eine eth1 hinzugefügt werden, die auf der vmbr1 hängt und virtio verwendet.

.. image:: http://freifunk-mk.de/gfx/proxmox-59.png

.. image:: http://freifunk-mk.de/gfx/proxmox-60.png

Danach die VM einmal durchbooten.


Eulenfunk BGP-Konzentrator-Konfigurator
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**Ist leider noch Baustelle hier...** Bis auf weiteres geht es mit unten bei ferm_einrichten_ weiter.

**Die genauen Hintergründe sollten verstanden werden und sind weiter unten beschrieben!**

Um die Konfiguration zu vereinfachen, wurde ein Script geschrieben, welches die nötigen Parameter abfragt und daraus die Konfigurationsdateien, bzw. Auszüge daraus erzeugt. Diese müssen dann nur noch an die richtige Stelle kopiert werden.

::

	sudo mkdir -p /opt/eulenfunk/konzentrator
	cd /opt/eulenfunk/konzentrator
	sudo git clone https://github.com/eulenfunk/ff-bgp-konzentrator-konfigurator.git
	cd ff-bgp-konzentrator-konfigurator
	sudo ./bgp-konzentrator-setup.sh

::

Das Script fragt dann die nötigen Werte ab.

Beschreibung der abgefragten Werte
..................................

Allgemeine Parameter
++++++++++++++++++++
AS Nummer vom FF-RL
	Hier wird die Nummer des autonomen Systems vom Freifunk Rheinland eingetragen. Aktuell ist das 201701.
Eigene AS Nummer
	Ihr benötigt ein eigenes autonomes System. Die Nummer davon gebt ihr hier an. TODO: Link auf Beschreibung zur Beschaffung eines eigenen AS...
Zugewiesene FFRL-IPV4-Exit-Adresse
	Vom Freifunk Rheinland bekommt ihr eine Exit-Adresse. Darauf wird der gesamte IPv4 Verkehr aller an diesem Konzentrator angeschlossenen Supernodes bzw. der darüber verbundenen Clients ge-NAT-ed. Diese Adresse sieht in etwa so aus: 185.66.19X.YY
Zugewiesenes FFRL-IPV6-Netz
	Der IPv6 Prefix, der euch vom Freifunk Rheinland zugewiesen wurde. (2a03:2260:XXX::/48)
Eigene öffentliche IPV4 Adresse
	Bei der Einrichtung der VM für diesen Konzentrator habt ihr eine IPv4-Adresse konfiguriert (Failover-IP der VM), über die ihr euch auch auf dem Konzentrator eingeloggt habt. Also die IPv4-Adresse von *eth1*.
Eigener SSH-Port
	Ihr habt bei der Konfiguration vom *sshd* den Port angepasst (62954), also gebt ihr diesen hier ein. Damit wird sichergestellt, dass die Firewall (ferm ...) Verbindungen zu dem alternativen Port überhaupt zulässt. Wenn ihr euch hier vertut, kommt ihr nach dem Neustart nicht mehr per SSH auf euren Server!

Konfiguration für GRE-Tunnel nach XXX_Y
+++++++++++++++++++++++++++++++++++++++
Ihr solltet vom Freifunk Rheinland Adressen für 4 Tunnel zum Backbone bekommen haben, jeweils zwei in Berlin und zwei in Düsseldorf. In diesem Abschnitt werden diese konfiguriert. Die folgenden Werte müsst ihr jeweils einmal pro Tunnel passend -- also 4 Mal -- eingeben:

IPV4 Adresse für Tunnelendpunkt auf Backbone-Server
	Die Tunnel-interne IPv4 Adresse auf dem **Backbone-Server** (100.64.X.YYY gerade).
IPV4 Adresse für Tunnelendpunk auf Konzentrator
	Die Tunnel-interne IPv4 Adresse für den Tunnelendpunkt auf **eurem Konzentrator** (10.64.X.ZZZ nächste ungerade).
IPV6 Adresse auf Backbone-Server
	Zusätzlich zu den IPv4-Adressen habt ihr eine IPv6 Adresse für den Tunnel bekommen. Die Adresse mit der ()...)::**1**/64  hinten ist die Adresse auf dem Backbone-Server (in etwa diese 2a03:2260:Y:XXX::1 ohne die /64!). Diese gebt ihr hier an.
IPV6 Adresse auf Konzentrator
		Die auf die im vorherigen Schritt folgende Addresse, also mit ()...)::**2**/64 hinten, ist die Adresse auf eurem Konzentrator (in etwa diese 2a03:2260:Y:XXX::2 ohne die /64!). Diese gebt ihr hier an.

Ausgaben
++++++++
Das Script erzeugt folgende Dateien:

* bird.conf.bgp
* bird6.conf.bgp
* interfaces.bgp
* ferm.conf.bgp
* 20-ff-config.conf.bgp

Die erzeugten Dateien sollten nun **überprüft** werden (Beschreibung hierzu siehe unten) und dann an die passenden Stellen kopiert werden:

::

	sudo cp bird.conf.bgp /etc/bird/bird.conf
	sudo cp bird6.conf.bgp /etc/bird/bird6.conf
	sudo mkdir /etc/ferm
	sudo cp ferm.conf.bgp /etc/ferm/ferm.conf
	sudo cp 20-ff-config.conf.bgp /etc/sysctl.d/20-ff-config.conf
	sudo cat interfaces.bgp >> /etc/network/interfaces

::

Da nun ein eventueller alternativer SSH-Port in die ferm.conf eingetragen wurde, kann das Firewalling aktiviert werden.

Als erstes ferm installieren.

::

	sudo apt-get install ferm

Bei der Frage, ob ferm beim Systemstart gestartet werden soll, mit ja antworten.

Danach kann das System rebootet werden. Die Konfigurationen für die Supernodes werden später wie unten beschrieben angelegt.

Routing
.......
Zum Routing werden Regeln benötigt, die die Pakete aus dem Freifunk Netz und die Pakete vom FFRL Backbone in eine gesonderte Tabelle (Tabelle 42) leiten. In dieser Tabelle wird vom bird per BGP eine Defaultroute ins Backbone gesetzt und manuell Routen zum eigenen Freifunk Netz (zu den Supernodes).

Um eine Menge Handarbeit zu sparen wird das Anlegen der Rules für die einzelnen Communities/Supernodes per Script erledigt:

::

	cd /opt/eulenfunk/konzentrator
	sudo git clone https://github.com/eulenfunk/konzentrator.git
	cd konzentrator
	sudo chmod +x *.sh
	sudo mkdir config


Damit das Script auch beim boot seine Arbeit verrichten kann muss es in die rc.local eingetragen werden.


::

	sudo nano /etc/rc.local


::

	#!/bin/sh -e
	# rc.local
	/opt/eulenfunk/konzentrator/konzentrator/bgp-konzentrator-rc.sh
	exit 0

Im Ordner **config** wird je Supernode ein config file angelegt. Die Beschreibung zum Hinzufügen von Supernodes erfolgt im Dokument "Supernode einrichten".


Monitoring
^^^^^^^^^^

Das Monitoring beinhaltet folgende Komponenten:

* Check_MK ermöglicht das zentrale Monitoring aller Systemdaten aller eingebundenen Server
* vnstat erstellt Traffic Statistiken, die sich auf der shell anzeigen lassen
* vnstati generiert daraus Grafiken
* lighttpd stellt diese zum Abruf aus dem Internet bereit

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

		only_from = 127.0.0.1 94.23.160.148

Damit diese Änderungen aktiviert werden, muss der xinetd durchgestartet werden

::

	sudo /etc/init.d/xinetd restart


Der Rechner hält ab nun Daten zum Abruf bereit.

JJX Bescheid sagen, der kümmert sich dann darum.

vnstat einrichten
.................
Alle 5 Minuten werden die Grafiken der Durchsatzdaten aktualisiert:

::

	sudo mkdir -p /var/www/vnstats/eth0
	sudo mkdir -p /var/www/vnstats/eth1
	sudo nano /etc/cron.d/vnstat

::

	*/5 * * * * root vnstati -i eth0 -o /var/www/vnstats/eth0/hours.png -h
	*/5 * * * * root vnstati -i eth0 -o /var/www/vnstats/eth0/days.png -d
	*/5 * * * * root vnstati -i eth0 -o /var/www/vnstats/eth0/months.png -m
	*/5 * * * * root vnstati -i eth0 -o /var/www/vnstats/eth0/summary.png -s
	*/5 * * * * root vnstati -i eth1 -o /var/www/vnstats/eth1/hours.png -h
	*/5 * * * * root vnstati -i eth1 -o /var/www/vnstats/eth1/days.png -d
	*/5 * * * * root vnstati -i eth1 -o /var/www/vnstats/eth1/months.png -m
	*/5 * * * * root vnstati -i eth1 -o /var/www/vnstats/eth1/summary.png -s
