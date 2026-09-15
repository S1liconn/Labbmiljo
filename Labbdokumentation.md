# Labbmiljö, Git, CLI och AI

**Kurs:** Introduktion till yrkesrollen och grunderna i IT-infrastruktur (MYH 2025/4008)

Detta är ett lab-experiment på att sätta upp en virtuell labbmiljö, dokumentera det under tiden genom Git, utföra uppgifter och felsöka genom kommandoraden i både Linux och Windows. 

**Labbmiljö & Nätverk**

| Hostname | Operativsystem | IP-adress | Subnätmask | Standardgateway |
| :--- | :--- | :--- | :--- | :--- |
| Ubuntu | Ubuntu 26.04 | 192.168.50.5 | 255.255.255.0 | 192.168.50.1 |
| Windows | Windows 11 | 192.168.50.202 | 255.255.255.0 | 192.168.50.1 |


Konfigurerade statiska IP-addresser på både Windows och Ubuntu för att undvika att IP-addresserna ändras övertid då de bestämdes innan av en DHCP-server. Genom inställningar appen på både Windows och Ubuntu, manuellt konfigurerades IP-addresserna till samma-addresser som DHCP gav ut.


**Kommandoradsgemonförande**  

**Linux:**  

Omdirigera kommandotolken till mappen var via cd, följt av skapandet av systemmentor med sudo mkdir eftersom vanliga användare saknar behörighet att göra ändringar där. Därefter sker en omdirigering till systemmentor med cd för att sedan skapa undermappen konsultdata med sudo mkdir, och slutligen omdirigeras det in i konsultdata med cd. 

En anteckningsfil skapas genom att använda nano-kommandot tillsammans med sudo nano anteckningar.txt där filen sparas med texten "Hej", medan användargruppen konsulter skapas genom att skriva sudo groupadd konsulter. Textfilen tilldelas behörigheter så att endast ägaren får skriva och ändra genom sudo chmod 640 anteckningar.txt.

Arbetet fortsätter genom att omdirigera bakåt med cd .. för att gå tillbaka till systemmentor och ändra behörigheterna för mappen konsultdata med sudo chmod 750 konsultdata. Kommandot ls -la bekräftar sedan ändringen med utdata som visar drwxr-x--- 2 root konsulter 4096 Sep 15 14:50 konsultdata, vilket innebär att det inte längre går att omdirigera till mappen som vanlig användare.  

**Verifiering av nätverksanslutning:**  
Ställde in bridged host med physical Connection.
Windows kan pinga Ubuntu, men Ubuntu kan inte pinga Windows.
Frågar Gemini vad det kan bero på, Gemini pekar på brandväggen hos Windows, blir föreslagen att aktivera regeln ICMPv4.
Aktiverar regeln ICMPv4 och plötsligt rullar all inkommande pingar in.