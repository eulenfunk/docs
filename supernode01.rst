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

Im nächsten Schritt wählt man VPS Proxmox VE 3.4 (64Bit) als Template aus, der Haken bei "Personalisierte Installation" darf NICHT gesetzt sein. Mit Klick auf "Weiter" startet man jetzt die Installation.

.. image:: http://freifunk-mk.de/gfx/sys02.png

Wenn die Installation seitens Soyoustart abgeschlossen ist, bekommt man eine Benachrichtigung per Mail.



SSH
^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface, trotzdem ist es wichtig, sich für Notfälle einen SSH Zugriff einzurichten und natürlich auch den SSH Server abzusichern.

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

				apt-get install sudo


Neuen User anlegen:

::

					useradd meinbenutzername


Den neuen User der Gruppe "sudo" hinzufügen:

	::

	        gpasswd -a meinbenutzername sudo


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

	Port 62954

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss.

Nun den direkten Rootlogin sperren.

::

	PermitRootLogin yes

ändern in

::

	PermitRootLogin no

Danach den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen.

::

	/etc/init.d/ssh restart

Den nachfolgenden ssh Kommandos muss man die Option "-p 62954" (kleines "p"!) und den scp Kommandos
die Option "-P 62954" (großes "P"!).

::

			ssh -p 62954 meinbenutzername@111.222.333.444



Updates einspielen
^^^^^^^^^^^^^^^^^^

Nun Betriebsystemupdates einspielen und ggf. erfolgende Rückfragen mit einem "J" oder "Y" abnicken, das "autoremove wird nicht viel tun, aber der Vollständigkeit halber sollte man es sich gleich angewöhnen.


::

        sudo apt-get update
        sudo apt-get dist-upgrade
        sudo apt-get autoremove


Eine Fehlermeldung im Bereich "Proxmox-Enterprise" kann man entweder ignorieren. Das gibt es nur wenn man ein Support-Abo abgeschlossen hat. Wenn Ihr die Arbeit des Proxmox-Teams unterstützen möchtet:

https://www.proxmox.com/de/proxmox-ve/preise


Optional:

Da einzelne Repositories wiederholt nicht oder sehr schlecht per IPv6 erreichbar sind und wir unsere Maschinen grundsätzlich zur IPv6-Nutzung befähigen, empfiehlt es sich, IPv6 zumindest für "apt-get" zu unterbinden.

Dazu wird einmalig aufgerufen:

::

	sudo ...!! SDFSDF echo 'Acquire::ForceIPv4 "true";' > /etc/apt/apt.conf.d/99force-ipv4


Monitoring
^^^^^^^^^^

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

        wget --no-check-certificate "https://monitoring.eulenfunk.de/heimathoster/check_mk/agents/check-mk-agent_1.2.8p1-1_all.deb"

Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum ausliefern der monitoring Daten. Die Installation von gdebi kann durchaus einige Dutzend Pakete holen. Das ist leider normal.
Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	sudo apt-get install gdebi-core xinetd lmsensors smartmontools 

Rückfragen ggf. mit "J" beantworten.
Mit dem nun installierten gdebi das check_mk-Paket installieren:

::

	sudo gdebi check-mk-agent_1.2.8p1-1_all.deb

Dann die Sensor-datenbank aktualisieren (Alle Rückfragen durch Eintippen von "yes" bestätigen)

::

	sudo sensors-detect

Abschließend dann den Service neu starten (Aufruf ist redundant) und die Ausgabe grob auf Plausiblität/Freiheit von internen Fehlermeldungen prüfen. 
 
 ::
 
        sudo service kmod start 
	sudo /etc/init.d/kmod start
	sensors

Nun noch zusätzliche Check_MK Plugins hinzufügen

::

        cd /usr/lib/check_mk_agent/plugins
        sudo wget --no-check-certificate "https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/plugins/smart"
        sudo chmod +x smart

				cd /usr/lib/check_mk_agent/local
        sudo wget --no-check-certificate https://raw.githubusercontent.com/eulenfunk/check_mk/master/proxmox
        sudo chmod +x proxmox

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
ISO Files zur installation können zwar über das Webinterface hochgeladen werden, aber je nach Internetanbindung dauert das lange. Per wget wird das Image direkt auf den Server geladen.

::

	cd /vz/template/iso
	wget http://releases.ubuntu.com/14.04.4/ubuntu-14.04.4-server-amd64.iso


OATH Two Factor
^^^^^^^^^^^^^^^

Der Zugang zum Proxmox ist absolut sicherheitskritisch, wer Zugriff auf den Hypervisor hat hat Zugriff auf alle Maschinen auf dem Blech. Daher muss zusätzlich der Login des Webinterface per OATH Two Factor Authentifizierung abgesichert werden.

-> https://pve.proxmox.com/wiki/Two-Factor_Authentication

Netzwerk einrichten
^^^^^^^^^^^^^^^^^^^

Ab jetzt geht die Konfiguration über das Proxmox Webinterface im Browser:

::

	https://111.222.333.444:8006

Beim ersten Aufruf sollte man das Zertifikat im Browser dauerhaft akzeptieren.

Die Anmeldung erfolgt mit Benutzername, Kennwort und OTP Pin.
Als Realm muss Linux PAM standard authentication (+ oath) ausgewählt werden.

.. image:: http://freifunk-mk.de/gfx/proxmox-1.png

----

Nachdem links in der Seitenleiste das Blech ausgewählt wurde rechts im Reiter Network zusätzlich zur vorhandenen vmbr0 über die das Internet rein kommt noch mindestens eine vmbr1 anlegen, über die die Supernodes mit dem Konzentrator kommunizieren.

Bei OVH/Soyoustart kann es sein, dass die vmbr schon vorhanden ist, dann müsst ihr nichts tun.

.. image:: http://freifunk-mk.de/gfx/proxmox-2.png

.. image:: http://freifunk-mk.de/gfx/proxmox-3.png

Beim Anlegen muss als Name vmbr1 eingetragen werden und der Haken bei Autostart gesetzt werden.

.. image:: http://freifunk-mk.de/gfx/proxmox-4.png
----

Die vmbr steht erst nach dem Neustart des Blechs zu Verfügung, daher in der Ecke oben rechts "Restart" auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-5.png
----

Backup anlegen
^^^^^^^^^^^^^^

Proxmox ermöglicht es ganz einfach und auf Wunsch automatisiert Backups von den Virtuellen Maschinen anzulegen.
Im Idealfall sollten die Backups auf einen externen Server/Storage erfolgen. Aus Gründen der Einfachheit beginnen wir mit einem Backup auf den lokalen Storage. Von dort kann man die Dateien für den Fall eines Totalausfalls des Blechs bei Bedarf per scp oder rsync auf einen anderen Server oder den heimischen Computer sichern.

Das Backup auf dem lokalen Storage erzeugt massiv IO, denn neben den normalen Zugriffen, die die Maschinen im Betrieb erzeugen kommen noch Lesezugriffe auf die zu sichernde VM und Schreibzugriffe auf die Backupdatei dazu.

Sobald der IO die Kapazität des Storages übersteigt, gerade bei den einfachen Raids aus klassischen HDDs in den OVH/SYS Servern ist dies schnell der Fall, wird die Performance des gesamten Blechs und aller VMs darunter leiden.

Das Backup sollte daher zur Zeit der geringsten Auslastung erfolgen, z.B. jeden Montag um 1 Uhr in der Nacht.

Zuerst muss ein Backupstorage definiert werden, dazu muss links das Datacenter ausgewählt werden, rechts der Tab Storage und dort der lokale Storage konfiguriert werden.

.. image:: http://freifunk-mk.de/gfx/px_backup01.png

Dort muss dann VZDump backup file zusätzlich ausgewählt werden (STRG+Klick)

.. image:: http://freifunk-mk.de/gfx/px_backup02.png

Als nächstes im Reiter Backup einen Backupjob hinzufügen. Bei Node wird "-- All --" und bei Mode Snapshot ausgewählt. Storage setzt man auf local. Als Compression wählt man "LZO (fast)" um die Prozessorauslastung gering zu halten.

.. image:: http://freifunk-mk.de/gfx/px_backup03.png

.. image:: http://freifunk-mk.de/gfx/px_backup04.png
