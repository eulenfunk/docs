Proxmox
=======

Einleitung
^^^^^^^^^^

Proxmox stellt alle Funktionen für den Betrieb von virtuellen Maschinen bereit und bietet per Webinterface eine zentrale Möglichkeit, neue VMs anzulegen und bestehende zu verwalten, inkl. einer KVM-Konsole für VMs und auch den Host selbst. Das funktioniert ohne Spezial-Plugins (d.h. kein Flash, keine JRE etc.)

Die Einrichtung des Proxmox beschränkt sich auf folgende Punkte:

* Installation: Hoster wie OVH/Soyoustart nehmen euch die Arbeit ab
* Einrichtung des SSH Zugriffs per Public-Key
* Absicherung des SSH Servers
* Absicherung des Webinterfaces per Two-Factor-Authentication (Oath)
* Einrichtung des Monitorings per Check_MK
* Bereitstellung der ISO Datei für Ubuntu Server

Installation
^^^^^^^^^^^^

Proxmox kommt entweder per Klick als Template vom Provider auf den Server oder muss von Hand installiert werden.

Hier ein Beispiel für die Installation über das Soyoustart Web-Frontend. Zunächst den passenden Server im Dropdown-Menü auswählen und dann auf "Installieren" klicken:

.. image:: http://freifunk-mk.de/gfx/sys01.png

Im nächsten Schritt wählt man VPS Proxmox VE 5.0 (64Bit) als Template aus, der Haken bei "Personalisierte Installation" darf NICHT gesetzt sein. Mit Klick auf "Weiter" startet man jetzt die Installation.

.. image:: http://freifunk-mk.de/gfx/sys02.png

Wenn die Installation seitens Soyoustart abgeschlossen ist, bekommt man eine Benachrichtigung per Mail.



SSH
^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface. Trotzdem ist es wichtig, sich für Notfälle einen SSH Zugriff einzurichten und natürlich auch den SSH Server abzusichern.

Per SSH mit dem Server verbinden

::

	ssh root@111.222.333.444

Kennwort ändern
...............

Wenn Proxmox durch den Hoster aufgesetzt wurde und das Kennwort per Mail kam, sollte es geändert werden mit passwd

::

		passwd


Normalen Useraccount anlegen
............................

Als zusätzliche Sicherheitsstufe wird der direkte root-Login per ssh komplett untersagt.
Der Login erfolgt dann über einen zusätzlich anzulegenden Benutzer. Dieser Benutzer muss über ein sicheres Passwort (TM) abgesichert werden. Nötige administrative Tätigkeiten werden mit sudo ausgeführt.

sudo installieren:

::

				apt install sudo


Neuen User anlegen:

::

					adduser meinbenutzername --ingroup sudo


::

	        cd /home/meinbenutzername/
	        mkdir .ssh
	        nano .ssh/authorized_keys

Im Editor dann den Public Key ("ssh-rsa AAA.....") einfügen. Wichtig: Alles von diesem Key muss in eine Zeile.
Jeder Administrator bekommt nach dem beschriebenen Verfahren seinen eigenen Account.

Nun das Password-Login auf dem Server deaktivieren. Dazu die sshd_config editieren:

::

	nano /etc/ssh/sshd_config

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

ändern z.B. in

::

	Port 45926

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss.

Nun den direkten Rootlogin sperren.

::

	PermitRootLogin yes

ändern in

::

	PermitRootLogin no

Danach den Editor wieder verlassen und den SSH Server neu starten, um die Einstellungen zu übernehmen.

::

	/etc/init.d/ssh restart

Den nachfolgenden ssh Kommandos muss man die Option "-p 45926" (kleines "p"!) und den scp Kommandos
die Option "-P 45926" (großes "P"!).

::

			ssh -p 45926 meinbenutzername@111.222.333.444



Updates einspielen
^^^^^^^^^^^^^^^^^^

Nun Betriebsystemupdates einspielen und ggf. erfolgende Rückfragen mit einem "J" oder "Y" abnicken, das "autoremove wird nicht viel tun, aber der Vollständigkeit halber sollte man es sich gleich angewöhnen.


::

        sudo apt update
        sudo apt dist-upgrade
        sudo apt autoremove


Eine Fehlermeldung im Bereich "Proxmox-Enterprise" kann man entweder ignorieren. Das gibt es nur wenn man ein Support-Abo abgeschlossen hat. Wenn Ihr die Arbeit des Proxmox-Teams unterstützen möchtet:

https://www.proxmox.com/de/proxmox-ve/preise


Monitoring
^^^^^^^^^^

Der Check_MK Agent steht in der Weboberfläche des Check_MK als .deb Paket bereit.

In die CheckMK-Instanz per Webbrowser einloggen.
Wer selbst kein Monitoring betreibt und auch keinen Zugang zum Eulenfunk Monitoring hat meldet sich beim Eulenfunk Admin Team.

Dann suchen:

::

        -> WATO Configuration (Menü/Box)
        -> Monitoring Agents
        -> Packet Agents
        -> check-mk-agent_1.4.0p8-1_all.deb (Die Versionsnummer kann abweichen)

Den Download-Link in die Zwischenablage kopieren.
Im SSH-Terminal nun eingeben: (die Download-URL ist individuell und der Name des .deb-Paketes ändert sich ggf.)

::

        wget https://monitoring.eulenfunk.de/eulenfunk/check_mk/agents/check-mk-agent_1.4.0p8-1_all.deb

Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum ausliefern der monitoring Daten.
Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	sudo apt-get install gdebi-core xinetd

Rückfragen ggf. mit "J" beantworten.
Mit dem nun installierten gdebi das check_mk-Paket installieren:

::

	sudo gdebi check-mk-agent_1.4.0p8-1_all.deb

Nun noch zusätzliche Check_MK Plugins hinzufügen

::

        cd /usr/lib/check_mk_agent/plugins
        sudo wget https://monitoring.eulenfunk.de/eulenfunk/check_mk/agents/plugins/smart
        sudo chmod +x smart

        cd /usr/lib/check_mk_agent/local
        sudo wget https://raw.githubusercontent.com/eulenfunk/check_mk/master/proxmox
        sudo chmod +x proxmox

Damit nicht jeder die Monitoring Daten von unserem Server abrufen kann, beschränken wir den Zugriff auf die IPv4 Adresse unseres Check_MK Servers.

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

Eulenfunker müssen dann das Admin-Team kontaktieren, damit der Rechner im CheckMK eintragen wird.


Images hochladen
^^^^^^^^^^^^^^^^
ISO Files zur installation können zwar über das Webinterface hochgeladen werden, aber je nach Internetanbindung dauert das lange. Per wget kann das Image direkt aus dem Internet auf den Server geladen werden.

::

	cd /vz/template/iso
	wget http://releases.ubuntu.com/16.04.2/ubuntu-16.04.2-server-amd64.iso


OATH Two Factor
^^^^^^^^^^^^^^^

Der Zugang zum Proxmox ist absolut sicherheitskritisch, wer Zugriff auf den Hypervisor hat, hat Zugriff auf alle Maschinen auf dem Blech. Daher muss zusätzlich der Login des Webinterface per OATH Two Factor Authentifizierung abgesichert werden.
Auf der CLI (per SSH) oathkeygen ausführen.

::

	$ oathkeygen
	SCI5UUB5XI6PGKAS

Den generierten Schlüssel merken.

Ab jetzt geht die Konfiguration über das Proxmox Webinterface im Browser:

::

	https://111.222.333.444:8006

Beim ersten Aufruf sollte man das Zertifikat im Browser dauerhaft akzeptieren.

Die Anmeldung erfolgt mit Benutzername (root) und dazugehörigem Kennwort.
Als Realm muss "Linux PAM standard authentication" ausgewählt werden.

.. image:: http://freifunk-mk.de/gfx/inlog.jpg

Zuerst legen wir für eine Gruppe für die Administratoren an.

"Datacenter" -> "Permissions" -> "Groups" -> "Create"

.. image:: http://freifunk-mk.de/gfx/groups.jpg

Der Gruppe müssen nun die notwendigen Berechtigungen hinzu gefügt werden.

"Datacenter" -> "Permissions" -> "Add" -> "Group Permission"

.. image:: http://freifunk-mk.de/gfx/permissions.jpg

Der "Path" wird auf "/" (das Wurzelverzeichnis) gesetzt
Als Gruppe wählt man die gerade erstellte "eulenadmins".
Proxmox ermöglicht ein sehr feingranulares Rollen und Rechte Konzept, wir wählen hier aber einfach "Administrator", damit dürfen alle Benutzer der Gruppe alles.

.. image:: http://freifunk-mk.de/gfx/permissions2.jpg

Nun muss der eigene Benutzer für angelegt werden.

"Datacenter" -> "Permissions" -> "Users" -> "Add"

.. image:: http://freifunk-mk.de/gfx/users.jpg

Der Benutzername muss exakt dem für den SSH Login verwendeten Benutzernamen entsprechen.
Als "Realm" muss "Linux PAM standard authentication" und als Gruppe die erstellte "eulenadmins" ausgewählt werden.
Der soeben generierte OATH Schlüssel wird nun im Feld "Key IDs" eingetragen.

.. image:: http://freifunk-mk.de/gfx/users2.jpg

Damit ie Zweifaktorauthentifizierung vollständig ist muss diese noch für die verwendete Login Methode aktiviert werden.

"Datacenter" -> "Permissions" -> "Authentication" -> "pam"

Als "TFA" muss "OATH" ausgewählt werden.

.. image:: http://freifunk-mk.de/gfx/tfa.jpg

Nun einmal abmelden "Logout" und als "meinbenutzername" unter Verwendung des von der OATH App generierten Schlüssels wieder anmelden.

Netzwerk einrichten
^^^^^^^^^^^^^^^^^^^

Für das geplante Setup wird eine zweite Netzwerkbrücke (vmbr) benötigt, diese kann über das Webinterface angelegt werden.

"Datacenter" -> "Servername" -> "System" -> "Network" -> "Create" -> "Linux Bridge"

Bei OVH/Soyoustart kann es sein, dass eine zweite vmbr (vmbr1) schon vorhanden ist, dann müsst ihr nichts tun.

.. image:: http://freifunk-mk.de/gfx/network.jpg

Beim Anlegen muss als Name vmbr1 eingetragen werden und der Haken bei Autostart gesetzt werden.

.. image:: http://freifunk-mk.de/gfx/network2.jpg

Die vmbr steht erst nach dem Neustart des Blechs zu Verfügung, daher in der Ecke oben rechts "Restart" auswählen.

Dann müssen wir einige Parameter in der "/etc/network/interfaces" Datei anpassen.

Da es sich bei der neuen Bridge um eine "anonyme" Bridge handelt, d.h. sie hat keine eigene IP-Adresse, sollte
der Parameter "bridge_maxwait 0" für die "vmbr1" gesetzt werden. Damit die Bridge keine IPv6 Konfiguration erhält,
tragen wir noch ein "post-up" Kommando ein (siehe unten).

Außerdem setzen wir noch die Parameter "bridge_ageing 0" und "bridge_maxage 0" für beide Bridges, um eventuellen
Konnektivitätsproblemen der VMs zuvorzukommen. Hier ein Ausschnitt aus der "/etc/network/interfaces" Datei, der
die Änderungen verdeutlicht:


::

	auto vmbr1
	iface vmbr1 inet manual
		bridge_ports dummy0
		bridge_stp off
		bridge_fd 0
		bridge_maxwait 0
		bridge_maxage 0
		bridge_ageing 0
		post-up echo 1 > /proc/sys/net/ipv6/conf/vmbr1/disable_ipv6

	auto vmbr0
	iface vmbr0 inet static
		(...)
		bridge_maxage 0
		bridge_ageing 0



Um eventuellen Problemen mit der Netzwerk-Konnektivität zuvorzukommen, setzen wir auf der

Automatisches VM Backup konfigurieren
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Proxmox ermöglicht es ganz einfach und auf Wunsch automatisiert Backups von den Virtuellen Maschinen anzulegen.
Im Idealfall sollten die Backups auf einen externen Server/Storage erfolgen. Aus Gründen der Einfachheit beginnen wir mit einem Backup auf den lokalen Storage. Von dort kann man die Dateien für den Fall eines Totalausfalls des Blechs bei Bedarf per scp oder rsync auf einen anderen Server oder den heimischen Computer sichern.

Das Backup auf dem lokalen Storage erzeugt massiv IO, denn neben den normalen Zugriffen, die die Maschinen im Betrieb erzeugen kommen noch Lesezugriffe auf die zu sichernde VM und Schreibzugriffe auf die Backupdatei dazu.

Sobald der IO die Kapazität des Storages übersteigt, gerade bei den einfachen Raids aus klassischen HDDs in den OVH/SYS Servern ist dies schnell der Fall, wird die Performance des gesamten Blechs und aller VMs darunter leiden.

Das Backup sollte daher zur Zeit der geringsten Auslastung erfolgen, z.B. jeden Montag um 1 Uhr in der Nacht.

Zuerst muss ein Backupstorage definiert werden.

"Datacenter" -> "Storage" -> "local"

Unter "Content" muss alles ausgewählt werden.

.. image:: http://freifunk-mk.de/gfx/backup.jpg

Nun fügen wir einen regelmäßigen Backup Job hinzu.

"Datacenter" -> "Backup" -> "Add"

.. image:: http://freifunk-mk.de/gfx/backup2.jpg
