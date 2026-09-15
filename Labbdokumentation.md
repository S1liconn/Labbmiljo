**2026-09-15 13:40-13:50**
Ställde in bridged host med physical Connection.
Windows kan pinga Ubuntu, men Ubuntu kan inte pinga Windows.
Frågar Gemini vad det kan bero på, Gemini pekar på brandväggen hos Windows, blir föreslagen att aktivera regeln ICMPv4.
Aktiverar regeln ICMPv4 och plötsligt rullar all inkommande pingar in.


| Hostname | Operativsystem | IP-adress | Subnätmask | Standardgateway |
| :--- | :--- | :--- | :--- | :--- |
| Ubuntu | Ubuntu 26.04 | 192.168.50.5 | 255.255.255.0 | 192.168.50.1 |
| Windows | Windows 11 | 192.168.50.202 | 255.255.255.0 | 192.168.50.1 |