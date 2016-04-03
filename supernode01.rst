Proxmox
=======

Einleitung
^^^^^^^^^^

Proxmox stellt alle Funktionen für den Betrieb von virtuellen Maschinen bereit und bietet per Webinterface eine zentrale Möglichkeit, neue VMs anzulegen und bestehende zu verwalten, inkl. einer KVM-Konsole für Gäste und auch den Host selbst. Das funktioniert ohne Spezial-Plugins (d.h. kein Flash, keine JRE etc.)

Die Einrichtung des Proxmox beschränkt sich auf folgende Punkte:

* Installation: Hoster wie OVH/Soyoustart nehmen euch die Arbeit ab
* Einrichtung des SSH Zugriffs per public Key
* Absicherung des SSH Servers
* Absicherung des Webinterface per two-factor (Oath)
* Einrichtung des Monitorings per Check MK
* Bereitstellung der iso Datei für Ubuntu Server

Installation
^^^^^^^^^^^^

Proxmox kommt entweder per Klick als Template vom Provider auf den Server oder muss von Hand installiert werden.

Bei manueller Installation Hilft die Proxmox Doku: https://pve.proxmox.com/wiki/Installation

Achtung: Hostname nachträglich ändern nur streng nach Promox-Howto sonst funktioniert die Weboberfläche nicht mehr. Hostname mit nicht nur im Proxmox-Webinterface geändert werden, sondern auch in /etc/hostname und vor allem /etc/hosts ("reverse-lookup" für 127.0.0.1 und die public-IPv4)

SSH
^^^

Im laufenden Betrieb erfolgt die komplette Konfiguration über das Webinterface, trotzdem ist es wichtig, sich für Notfälle einen SSH Zugriff einzurichten und natürlich auch den SSH Server abzusichern.

Per SSH mit dem Server verbinden

::
	
	ssh root@111.222.333.444

Nun den SSH Public Key auf dem Server hinterlegen

::

	mkdir .ssh
	cd .ssh
	nano authorized_keys

In die noch leere Datei den Key eintragen und den Editor wieder verlassen (strg+x).

(Per default liegt hier eventuell schon ein Schlüssel drin. Dieser gehört dem Wartungssystem des jeweiligen Hosters. Über den Sinn und die Berechtigung dann man unterschiedlilche Meinungen haben. Ob man diesen drin lässt muss individuell entschieden werden.)

Als nächstes die SSH Verbindung beenden

::

	exit

Und unter Verwendung des SSH Keys erneut verbinden

::

	ssh root@111.222.333.444

Wenn der Key nicht als default im System hinterlegt ist muss zusätzlich der Pfad zum Key angeben werden.
Liegt der Key meinsshkey im Benutzerordner

::

	ssh -i ~/meinsshkey root@111.222.333.444

Nun den Password login auf dem Server deaktivieren, dazu die sshd_config editieren

::

	nano /etc/ssh/sshd_config

Die Zeile

::

	#PasswordAuthentication yes

ändern in

::

	PasswordAuthentication no

Achtung, auch wenn yes auskommentiert ist, besteht die Möglichkeit sich per Password zu verbinden, erst wenn 'no' gesetzt ist und nicht (mehr) auskommentiert ist, ist der Zugriff nur noch per Key möglich.

Den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen


::

	/etc/init.d/ssh restart

Kein direkten Root-Login erlauben
.................................

Als zusätzliche Sicherheitsstufe ist es empfehlenswert, (direkte) root-Logins per ssh komplett untersagen. 
Dann muss der Login über einen zusätzlich anzulegenden Benutzer (sshkey siehe oben) erfolgen. 
Zudem hinreichend sicheres Passwort setzen und den User in die sudoers-Gruppe aufnehmen. 

::
        
        adduser charly

.. image:: http://i.imgur.com/mWhOtNO.png      

::
        
        apt-get install sudo
       
gefolgt von 

::      
        
        sudo adduser charly sudo
        su charly
        cd /home/charly/
        mkdir .ssh
        nano .ssh/authorized_keys
        
Im Editor dann den public-ssh-Key ("ssh-rsa AAA.....") einfügen. Wichtig: Alles von diesem Key muss auf eine Zeile. 
Wenn es mehrere Leute gibt, die Zugriff haben sollen, dann pro Login-Key natürlich eine neue Zeile.
        

Nun den direkten Rootlogin sperren

:: 

        nano /etc/ssh/sshd_config

::

	PermitRootLogin yes
        
ändern in

::

	PermitRootLogin no

Abschließend: 

::

	/etc/init.d/ssh restart



Sinnvoll: Den SSH-Port ändern
.............................

Um es den Script-Kiddies und Bots etwas schwerer zu machen, sollte der Port 22 auf einen hohen Port (mindestens über 1024) verändert werden. Dazu die Zeile

::

	Port 22
        
ändern z.B. in

::

	Port 62954

WICHTIG: Diesen Port muss man sich dann merken, da man ihn später beim Aufruf von ssh angeben muss.

Danach den Editor wieder verlassen und den SSH Server neu starten um die Einstellungen zu übernehmen.
Den nachfolgenden ssh Kommandos muss man die Option "-p 62954" (kleines "p"!) und den scp Kommandos
die Option "-P 62954" (großes "P"!).

Z.B.:

::

        ssh -p 62954 root@111.222.333.444

Kennwort ändern
^^^^^^^^^^^^^^^
Wenn Proxmox durch den Hoster aufgesetzt wurde und das Kennwort per Mail kam, sollte es geändert werden mit passwd

::

	passwd

Updates einspielen
^^^^^^^^^^^^^^^^^^

Nun Betriebsystemupdates einspielen und ggf. erfolgende Rückfragen mit einem "J" oder "Y" abnicken, das "autoremove wird nicht viel tun, aber der Vollständigkeit halber sollte man es sich gleich angewöhnen.


:: 

        sudo apt-get updates
        sudo apt-get dist-upgrade
        sudo apt-get autoremove
        

Eine Fehlermeldung im Bereich "Proxmox-Enterprise" kann man entweder ignorieren. Das gibt es nur wenn man ein Support-Abo abgeschlossen hat. Wenn Ihr die Arbeit des Proxmox-Teams unterstützen möchtet:

https://www.proxmox.com/de/proxmox-ve/preise


Monitoring
^^^^^^^^^^

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

        wget --no-check-certificate "https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/check-mk-agent_1.2.6p15-1_all.deb"

Um das .deb Paket zu installieren wird gdebi empfohlen, ausserdem benötigt der Agent xinetd zum ausliefern der monitoring Daten. Die Installation von gdebi kann durchaus einige Dutzend Pakete holen. Das ist leider normal. 
Per SSH auf dem Server. (Auch hier: Name des .deb-Files ggf. anpassen)

::

	apt-get install gdebi xinetd
	
Rückfragen ggf. mit "J" beantworten. 
Mit dem nun installierten gdebi das checkmk-Paket installieren: 

::
	
	gdebi check-mk-agent_1.2.6p15-1_all.deb

Nun ggf. noch die Smart-Überwachung der Festplatten hinzufügen

:: 
        
        cd /usr/lib/check_mk_agent/plugins
        wget --no-check-certificate "https://monitoring.freifunk-mk.de/heimathoster/check_mk/agents/plugins/smart"
        chmod +x smart

Der Rechner hält ab nun Daten zum Abruf bereit. 

_ToDo: Neuen Rechner im CheckMK eintragen in richtige Gruppe & Monitoring scharf schalten.

LetsEncrypt-Certifikat für den Proxmox
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
(optional)

Standardmäßig kommt die Webkonsole des Proxmox mit einem "selbstsignierten" SSL-Zertifikat daher. 
Das ist jedoch mindestens unschön, sondern ein Nutzungshindernis in bestimmten Umgebungen. 

Wenn ihr einen Domain-Hostnamen  (DNS A-record) setzen könnt, dann solltet ihr es tun und ein LE-Zertificat installieren

**Schritt 1: DNS A-record setzen**

Vergebt einen Hostnamen in dem von Euch genutzten DNS-Server (z.B. Provider-Webinterface) für die IP-Adresse. 
Dafür fügt ihr in der Domain (z.B. ffdus.de) einen neuen A-Record hinzu


.. image :: http://i.imgur.com/dLe1tqm.png

dann dort Werte hinterlegen. 

.. image :: http://i.imgur.com/dRHwsVs.png

und speichern 

.. image :: http://i.imgur.com/jpZIVih.png


Abschliessend testen, ob der Host auch erreichbar ist. 
Von einem anderen host (z.B. dem heimischen Rechner) 

::
	
	ping ffdus-pm.twin2.ffdus.de
	
.. image :: http://i.imgur.com/hffSyAY.png	

Bei Erfolg

**Schritt 2: Letsencrypt einrichten**

Wir benötigen _git_ (Rückfragen mit "J" beantworten)

::

        cd ~
	apt-get install git

nun wird das aktuele Letsencrypt aus dem git-repositry geholt

::

	git clone https://github.com/letsencrypt/letsencrypt

Nun brauchen wir noch ein Script, welches die notwendigen Folgeschritte übernimmt. 

:: 

        pico /root/le-renew.sh

Bitte im Script den **gewählten hostnamen austauschen**
        
::

	#!/bin/bash
	FQDN=ffdus-pm-twin2.ffdus.de
	cd /root/letsencrypt
	./letsencrypt-auto certonly --standalone --standalone-supported-challenges http-01 -d $FQDN
	rm /etc/pve/pve-root-ca.pem
	rm /etc/pve/local/pve-ssl.key
	rm /etc/pve/local/pve-ssl.pem
	cd /etc/letsencrypt/live/$FQDN
	cp chain.pem /etc/pve/pve-root-ca.pem
	cp fullchain.pem /etc/pve/local/pve-ssl.key
	cp fullchain.pem /etc/pve/local/pveproxy-ssl.pem
	cp privkey.pem /etc/pve/local/pveproxy-ssl.key
	cp cert.pem /etc/pve/local/pve-ssl.pem
	service pveproxy restart
	service pveproxy status
	service pvedaemon restart

Das script ausführbar machen 

::

        chmod +x ./le-renew.sh
        
Und einmal starten:

::

       ./le-renew.sh
       
Dabei gibt es ggf. einige Rückfragen, z.B. nach einer E-Mail-Adresse. 

Diese sollte eine sein, die auch gelesen wird. Denn dort gibt LetsEncrypt "Bescheid", wenn das Certifikat abläuft und man sich um eine Erneuerung kümmern sollte. 

.. image :: http://i.imgur.com/MQyGAn8.png

Login auf dem Proxmox sollte nun ohne SSL-Rückfragen auf (hier) https://ffdus-pm-twin2.ffdus.de:8006 möglich sein


Images hochladen
^^^^^^^^^^^^^^^^
Iso Files zur installation können zwar über das Webinterface hochgeladen werden, aber je nach Internetanbindung dauert das lange. Per wget wird das Image direkt auf den Server geladen.

::
	
	cd /vz/template/iso
	wget http://releases.ubuntu.com/14.04.4/ubuntu-14.04.4-server-amd64.iso


OATH Two Factor
^^^^^^^^^^^^^^^

Der Zugang zum Proxmox ist absolut sicherheitskritisch, wer Zugriff auf den Hypervisor hat hat Zugriff auf alle Maschinen auf dem Blech. Ihr solltet daher zusätzlich den Login des Webinterface per OATH Two Factor Authentifizierung absichern.

-> https://pve.proxmox.com/wiki/Two-Factor_Authentication

Netzwerk einrichten
^^^^^^^^^^^^^^^^^^^
Ab jetzt geht die Konfiguration über das Proxmox Webinterface im Browser:

::

	https://111.222.333.444:8006

Die Anmeldung erfolgt mit Benutzername und Kennwort und gegebenenfalls mit OATH Pin.

.. image:: http://freifunk-mk.de/gfx/proxmox-1.png
----

Nachdem links in der Seitenleiste das Blech ausgewählt wurde rechts im Reiter Network zusätzlich zur vorhandenen vmbr0 über die das Internet rein kommt noch mindestens eine vmbr1 anlegen, über die die Supernodes mit dem Backbone Server kommunizieren.

Bei OVH/Soyoustart kann es sein, dass die vmbr schon vorhanden ist, dann müsst ihr nichts tun

.. image:: http://freifunk-mk.de/gfx/proxmox-2.png

.. image:: http://freifunk-mk.de/gfx/proxmox-3.png

.. image:: http://freifunk-mk.de/gfx/proxmox-4.png
----

Die vmbr steht erst nach dem Neustart des Blechs zu Verfügung, daher in der Ecke oben rechts restart auswählen.

.. image:: http://freifunk-mk.de/gfx/proxmox-5.png
----

