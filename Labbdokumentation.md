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

**Windows:**  
Terminal öppnades för att kunna använda både PowerShell och Kommandotolken. Kommandotolken omdirigerades till C: med cd C:\, följt av skapandet av mappen Systemmentor med mkdir Systementor. Efter en omdirigering till den mappen skapades undermappen KonsultData med mkdir KonsultData. Därefter bytte fliken till Windows PowerShell där en omdirigering gjordes till konsultdata-mappen med cd C:\Systementor\KonsultData, varefter kommandot Get-acl kördes för att hämta behörigheterna.

**AI-stöd & Kritisk Utvärdering**   
Gemini var matad prompten: "Kan du förklara hur Linux behörighetsfunktion med chmod fungerar, vad de tre siffrorna (t.ex. 750) betyder, och hur jag använder kommandot i praktiken?"

```
Linux behörighetssystem är grundläggande för att kontrollera vem som kan läsa, skriva eller köra filer och mappar. Systemet bygger på tre roller och tre grundläggande handlingar.

1. Roller och handlingar

För varje fil och mapp delas behörigheterna upp i tre kategorier:

* U (User / Ägare): Den enskilda användare som äger filen.
* G (Group / Grupp): Den användargrupp som filen är kopplad till.
* O (Others / Övriga): Alla andra användare på systemet.

De handlingar som kan utföras är:

* Läs (Read - r): Möjlighet att öppna och läsa filens innehåll (eller lista innehållet i en mapp). Värde: 4.
* Skriv (Write - w): Möjlighet att ändra, radera eller spara i filen (eller skapa/ta bort filer i en mapp). Värde: 2.
* Kör (Execute - x): Möjlighet att köra filen som ett program/skript (eller "gå in i" en mapp med cd). Värde: 1.

2. Vad de tre siffrorna betyder (t.ex. 750)

När du ser ett kommando som chmod 750 använder du oktalt (numeriskt) läge. Varje siffra representerar summan av behörigheterna för en specifik roll:

1. Första siffran (7): Ägarens (User) behörighet.
2. Andra siffran (5): Gruppens (Group) behörighet.
3. Tredje siffran (0): Övrigas (Others) behörighet.

Siffrorna räknas fram genom att addera värdena för läs (4), skriv (2) och kör (1):

* 7 = 4 + 2 + 1 (Fullständiga behörigheter: läsa, skriva, köra)
* 5 = 4 + 0 + 1 (Läsa och köra, men inte skriva)
* 0 = 0 + 0 + 0 (Inga behörigheter alls)

Med andra ord (750): Ägaren kan göra allt (7), gruppen kan läsa och köra (5), och alla andra har ingen tillgång alls (0).

3. Så använder du chmod i praktiken

Kommandot chmod (change mode) används i terminalen för att ändra dessa rättigheter. Det finns två huvudsakliga sätt att göra det på:

A. Numeriskt läge (snabbast och vanligast)
Du anger direkt de tre siffrorna följt av fil- eller mognamnet:
chmod 750 minfil.sh

* Vill du göra en fil läsbar och skrivbar enbart för dig själv (och spärra för alla andra)? Använd 600.
* Vill du att alla ska kunna läsa och köra filen, men bara du ska kunna ändra den (vanligt för skript)? Använd 755.
* Standard för vanliga textfiler brukar vara 644 (ägaren kan läsa/skriva, alla andra kan bara läsa).

B. Symboliskt läge (mer läsbart)
Om du inte vill räkna ut siffror kan du använda bokstäver för att lägga till (+) eller ta bort (-) behörigheter:

* u = user, g = group, o = others, a = all
* r = read, w = write, x = execute

Exempel:

# Ge gruppen körrättighet på en fil

chmod g+x skript.sh

# Ta bort all behörighet för övriga ("others")

chmod o-rwx hemligt.txt

# Ge ägaren fullständiga rättigheter

chmod u=rwx dokument.txt

Tips: Rekursiva ändringar (-R)
Om du vill ändra behörigheter på en hel mapp och allt dess innehåll (undermappar och filer) använder du flaggan -R:
chmod -R 755 minmapp/
```

När jag återskapar kommandot genom att skapa en ny katalog i huvudanvändarens dokument katalog med namnet "Arkivet", sedan skapa en textfil med Hej.txt. 