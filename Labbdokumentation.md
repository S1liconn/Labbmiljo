# Labbmiljö, Git, CLI och AI

**Kurs:** Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)

Detta är ett lab-experiment på att sätta upp en virtuell labbmiljö, dokumentera det under tiden genom Git, utföra uppgifter och felsöka genom kommandoraden i både Linux och Windows. 

**Labbmiljö & Nätverk**

| Hostname | Operativsystem | IP-adress | Subnätmask | Standardgateway |
| :--- | :--- | :--- | :--- | :--- |
| Ubuntu | Ubuntu 26.04 | 192.168.50.5 | 255.255.255.0 | 192.168.50.1 |
| Windows | Windows 11 | 192.168.50.202 | 255.255.255.0 | 192.168.50.1 |


Ställde in bridged host med physical Connection.
Windows kan pinga Ubuntu, men Ubuntu kan inte pinga Windows.
Frågar Gemini vad det kan bero på, Gemini pekar på brandväggen hos Windows, blir föreslagen att aktivera regeln ICMPv4.
Aktiverar regeln ICMPv4 och plötsligt rullar all inkommande pingar in.

Konfigurerade statiska IP-addresser på både Windows och Ubuntu för att undvika att IP-addresserna ändras övertid då de bestämdes innan av en DHCP-server. Genom inställningar appen på både Windows och Ubuntu, manuellt konfigurerades IP-addresserna till samma-addresser som DHCP gav ut.