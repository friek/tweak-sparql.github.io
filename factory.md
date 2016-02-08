---
layout: page
title: Factory reset Zyxel
permalink: /factory/
---

Zorg dat je voordat je hier mee begint de standaard configuratie en firmware van Tweak gedownload hebt. Mocht er iets mis gaan, dan kun je altijd terug.


Telnet naar router en log in met admin

```
$ telnet 192.168.1.1
Login: admin
Password:
> save_default clean
ROM-D cleaned.
> restoredefault
```

Hierna is het het beste om een 30-30-30 reset te doen. De procedure hiervoor is:

* druk het reset knopje in en wacht 30 seconden
* hou het knopje ingedrukt, haal de stroom eraf en wacht 30 seconden
* met het knopje nog steeds ingedrukt, zet de stroom er weer op en wacht 30 seconden

Hiermee zorg je ervoor dat er niets in het geheugen blijft hangen wat voor problemen kan zorgen.

Als eerste moeten er de juiste WAN interfaces aangemaakt worden.
Ga naar **Network Setting > Broadband** en kies "Add New WAN Interface"

Voor internet (alleen de waarden die ingevuld moeten worden):

```
General
Active: 	Aan
Name:		ETHWAN (of een eigen gekozen naam)
Type:		Ethernet
Mode:		Routing
Encapsulation:	IPoE

Routing Feature
NAT Enable:			Aan
Fullcone NAT Enable:		Aan
IGMP Proxy Enable:		Uit!
Apply as Default Gateway:	Aan

VLAN
Active:	Aan
802.1p:	1
802.1q: 34
```

Voor IPTV (ook weer alleen de waarden die ingevuld moeten worden):

```
General
Active:		Aan
Name: 		IPTV (of een eigen gekozen naam)
Type: 		Ethernet
Mode: 		Routing
Encapsulation: 	IPoE

Routing Feature
NAT Enable:			Aan
Fullcone NAT Enable:		Aan
IGMP Proxy Enable:		Aan
Apply as Default Gateway:	Uit!

VLAN
Active: Aan
802.1p:	5
802.1q: 4
```

Vervolgens moet er een static route aangemaakt worden voor IPTV:
Ga naar **Network Setting > Routing** en "Add New Static Route"

```
Active:			Aan
Route name:		IPTV (of een eigen gekozen naam)
IP Type: 		IPv4
Destination IP Address:	185.6.48.0
IP Subnet Mask: 	255.255.255.0
Use Gateway IP Address:	Enable
Gateway IP Address: 	(kan leeg gelaten worden, deze vult hij automatisch in)
Use Interface: 		IPTV/eth4.2
```

Vanaf dit punt zou internet en TV moeten functioneren. Dan kan nu telefonie ingesteld worden.

Ga naar **VoIP > SIP > SIP Service provider** en kies voor "Add new provider"
```
SIP Service Provider Name: 	Tweak
SIP Server Address:		sip.tweakphone.nl
REGISTER Server Address: 	sip.tweakphone.nl
SIP Service Domain: 		sip.tweakphone.nl
```


Ga naar **VoIP > SIP > SIP Account** en kies voor "Add new account"

```
SIP Account Associated with:	Tweak
Enable SIP Account:		Aan
SIP Account Number:		31xxxxxxxxx
Username:			31xxxxxxxxx
Password:			wachtwoord
```

Als het goed is moet dan ook telefonie werken.
