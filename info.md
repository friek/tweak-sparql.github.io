---
layout: page
title: Netwerk info
permalink: /info/
---

TODO: hier komt een duidelijkere uitleg dan wat er op https://blog.tweak.nl/hardware/vlan-configuratie-bij-gebruik-eigen-apparatuur/ staat.
Ook is het de bedoeling dat hier straks configuratie gegevens komen voor bijvoorbeeld OpenWRT.

Bij Tweak wordt er gebruik gemaakt van VLAN's om het internet en IPTV te scheiden. Wil je eigen apparatuur gebruiken dan is het een vereiste dat de router overweg kan met 802.1Q.

## Internet
Voor internet kunnen de volgende instellingen gebruikt worden:

```
Type:     DHCP
VLAN id:  34
802.1P:   1
```

De DCHP lease is semi-static en gebonden aan het MAC adres. Alleen als je een ander MAC adres gebruikt of voor lange tijd geen verbinding hebt kan het IP-adres veranderen.

## IPTV
Voor IPTV worden de volgende instellingen gebruikt.

```
Type:     DHCP
VLAN id:  4
802.1P:   5
```

Het is belangrijk dat de gateway voor IPTV niet wordt gebruikt als default gateway.

De IPTV boxen maken gebruik van het internet om de interface en EPG op te halen, de TV streams moeten dan vanuit het IPTV VLAN komen. Om dit te bewerkstelligen moet er een static route en een IGMP proxy worden toegevoegd.

Voor de static route moet 185.6.48.0/26 gerouted worden naar de gateway van het IPTV VLAN.
