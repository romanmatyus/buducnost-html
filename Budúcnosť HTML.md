% Budúcnosť HTML
% Roman Mátyus

#Predstavenie HTML5

V súvislosti s novinkami okolo webových prehliadačov a všeobecne webu je v posledných rokoch najskloňovanejšou skratkou HTML5. 

HTML5 už neoznačuje iba novú generáciu pôvodného značkovacieho jazyka HTML[^1], ale obrovskú množinu pridružených technológií. Prirodzené smerovanie vývoja špecifikácie bolo od prvotného návru výrazne zmenené. V roku 1992[^2] keď bol predložený návrh prvých tagov[^3] si sotva niekto predstavoval súčasnú rozšírenosť internetu v smartfónoch a tabletoch.

[^1]: HyperText Markup Language - Hypertextový značkovací jazyk
[^2]: HTML Tags - [http://www.w3.org/History/19921103-hypertext/hypertext/WWW/MarkUp/Tags.html]()
[^3]: značiek

Takmer všetky technológie ponímané v skupine HTML5 prinášajú vlastne nové možnosti využitia JavaScriptu. Sprístupňujú nové JS API pre používanie databáz, hardvéru, funkcionalít operačného systému a.i. Iba malá časť špecifikácie HTML5 sa týka rozšírenia samotného značkovacieho jazyka.

Cieľom nových špecifikácií je zvýšenie bezpečnosti a komfortu ako vývojárov tak používateľov. Vývoj zastrešujú organizácie [W3C](http://w3c.org) a [WHATWG](http://www.whatwg.org/) a je dostupný na [github.com/w3c/html](https://github.com/w3c/html). Rôzne časti špecifikácie sú na rôznom stupni dokončenia. Našťastie je veľké množstvo častí špecifikácií implementovaných v aktuálnych verziách prehliadačov, takže je možné tieto technológie v praxi používať.

Niektoré technológie bežne zaraďované do technológií HTML5 nepochádzajú od W3C a ani neboli zatiaľ touto organizáciou prijaté za oficiálne. Sú pre ne vytvorené špeciálne združenia ktoré vyvíjajú špecifikácie, snažia sa ich presadiť ako oficiálne a implementovať ich do čo najväčšieho množstva prehliadačov. Príkladom je štandard WebRTC na komunikáciu medzi prehliadačmi bez potreby pluginov z dielne Googlu.

#Bezpečnosť

S rozširujúcimi možnosťami ktoré tieto technológie prinášajú prichádza zvýšené riziko bezpečnostných problémov. Prehľad niektorých týchto problémov je možné vidieť na [html5sec.org](http://html5sec.org/). Väčšinou je riešenie týchto problémov veľmi zložité, pretože nejde o chyby, ale vlastnosti, ktoré môžu byť v určitých prípadoch zneužité.

Následkom bezpečnostných problémov môže byť odcudzenie súkromných dát alebo extrémne zaťaženie systému.

##Sandbox iframe

Súčasťou takmer každého webu je kód tretej strany. Ide zväčša o pluginy sociálnych sietí alebo rôznych poskytovateľov doplnkov ako napríklad kalendárov, diskusií alebo panelu s počasím. Tieto doplnky sú do webov vkladané prostredníctvom `iframe`-ov - vložených fragmentov cudzích stránok. Tento prístup je potenciálne nebezpečný, pretože autor webu nemá plnú kontrolu nad obsahom vkladaného obsahu. Nahradenie kódu doplnku za škodlivý by si autor vôbec nemusel všimnúť.

K tomuto účelu bola vyvinutá špecifikácia na uzatvorenie iframov do sandboxu[^sandbox]. Prostredníctvom tejto špecifikácie je možné nastaviť minimálne potrebné práva pre `iframe`. V prípade vloženia škodlivého kódu do doplnku je týmto zamedzené škodám, pretože doplnok nemá oprávnenie nejakú škodu spôsobiť. Je vhodné nastaviť obmedzenia čo najprísnejšie. Po aplikovaní sandboxu na `iframe` je zakázaná všetka potenciálne nebezpečná činnosť. Ak doplnok potrebuje odosielať formulár alebo otvoriť vyskakovacie okno, tieto práva musia byť explicitne vymenované.[^sandbox-zdroj]

**Príklad:**

	<iframe sandbox allow-forms allow-popups></iframe>

[^sandbox]: virtuálny priestor bez prístupu k okoliu
[^sandbox-zdroj]: http://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/

#Komfort

Nezanedbateľnou nutnosťou vývoja HTML je zvýšenie používateľského komfortu. Možnosti ktoré dnes bežne na internete používatelia používajú priniesli do prehliadačov doplnky ako Flash, Java pluginy prípadne rôzne JavaScriptové knižnice. 

Na trhu vznikla požiadavka používať internet multimediálne, na čo nebol pôvodne navrhnutý. Tento nedostatok je aj v súčasnosti často odstraňovaný Flash prehrávačmi. S používaním webaplikácií prišli požiadavky na jednoduchšie zadávanie údajov do formulárov prípadne používanie animácií a rôznych grafických prechodov.

##Nové formuláre

Vzhľadom na výrazné zastúpenie dotykových zariadení pristupujúcich k webu, je vhodné dodať zariadeniu informáciu o možných vstupných znakoch. Toto elegantne rieši HTML5. Je zbytočné zobraziť používateľovi pri vypĺňaní telefónneho čísla `qwerty` klávesnicu.

###Typy formulárov

Moderné prehliadače pri použití nové formulárových prvkov automaticky prispôsobia ovládacie prvky tak, aby boli čo najpoužiteľnejšie. Dôležitým vylepšením je automatická navyše vrstva validácie na strane prehliadača. V prípade zadania nesprávnych údajov do poľa je na to používateľ upozornený. To všetko bez toho, aby vývojár písal obslužný validátor.

Nové typy vstupných polí podla cieľu použitia sú:

- `search` - pole vyhľadávania
- `email` - mailová adresa
- `url` - web adresa
- `tel` - telefónne číslo
- `number` - číslo
- `range` - číslo v rozsahu
- `date` - dátum
- `month` - mesiac
- `week` - týždeň
- `time` - čas
- `datetime` - dátum a čas
- `datetime-local` - dátum a čas bez časovej zóny
- `color` - farba

Niektoré problémy nie sú zatiaľ úplne doriešené.

Aktuálne verzie prehliadačov Firefox, Safari a Chrome majú napríklad problémy s viacbajtovými znakmi v doménach pri validácií mailu. Tento problém je manuálne riešiteľný. Predmetnému vstupnému polu sa dá nastaviť nový formát adresy pomocou regulárneho výrazu.

Ďalším problémom je, že formulárové prvky na zadanie dátumu a času majú presne stanovený formát. Môže to byť problém pre lokálnych používateľov.

Ak prehliadač typ formulárového prvku nepodporuje, je použité klasické pole `text`.[^nove-formulare]

[^nove-formulare]: http://html5doctor.com/html5-forms-input-types/

###Atribúty formulárov

S novými formulárovými typmi prišli aj nové atribúty, ktoré upravujú možnosti ich použitia.[^formularove-atributy]

- `placeholder` - nastavený text sa zobrazí kým nie je pole aktívne
- `autofocus` - automatické aktivovanie pola
- `autocomplete` - poskytne na výber skôr zadané vstupy - touto voľbou je možné funkciu vypnúť
- `required` - pole je pred odoslaním nutné vyplniť
- `pattern` - vstup musí zodpovedať nastavenému regulárnemu výrazu
- `list` - umožňuje nastaviť zoznam *našepkaných* vstupov
- `multiple` - umožní vybrať viac vstupov napríklad z *našepkaných* alebo viac súborov na odoslanie
- `novalidate` - pole sa nebude validovať
- `formnovalidate` - formulár sa nebude validovať
- `form` - prepojenie formulárového prvku mimo formulára s rodičovským formulárom
- `formaction` - nastavuje cieľ dát z formulára
- `formenctype` - nastavuje kódovanie dát z formulára
- `formmethod` - nastavuje spôsob odoslania formulára
- `formtarget` - nastavuje okno kde sa zobrazí výsledok spracovania


[^formularove-atributy]: http://html5doctor.com/html5-forms-introduction-and-new-attributes/

##Geolokácia

So stále rastúcim zastúpením smartfónov a tabletov na trhu postupne prišla požiadavka na zisťovanie polohy používateľa. V minulosti museli aj čisto webové aplikácie riešiť zisťovanie polohy pomocou natívneho programu. Vďaka [Geolocation API](http://dev.w3.org/geo/api/spec-source.html) to už nie je potrebné.

Vzhľadom na ochranu osobných údajov je samozrejmosťou v prípade snahy o prístup ku geolokačným dátam výzva na schválenie žiadosti.

API sprístupňuje jednoduchý objekt `navigator.geolocation` bežiacemu JavaScriptu. V prípade existencie tohoto objektu sú sprístupnené jeho metódy.[^geolokacia-zdrojak][^geolokacia-w3c][^geolokacia-mozila]

[^geolokacia-zdrojak]: http://www.zdrojak.cz/clanky/geolokace-v-prohlizeci/
[^geolokacia-w3c]: http://dev.w3.org/geo/api/spec-source.html
[^geolokacia-mozila]: https://developer.mozilla.org/en-US/docs/WebAPI/Using_geolocation

###Aktuálna pozícia

Metóda `navigator.geolocation.getCurrentPosition()` vráti zadanému `callback`u súradnice kde sa aktuálne zariadenie nachádza. Dodaný objekt obsahuje informácie o zemepisnej šírke a dĺžke, nadmorskej výške, presnosti merania, azimute smeru pohybu a jeho rýchlosti.

###Sledovanie pohybu

Metóda `navigator.geolocation.watchPosition()` je totožná s predošlou, s tým rozdielom, že sa callback pre spracovanie údajov volá periodicky. Návratovou hodnotou je identifikátor sledovania. Ten je možné použiť v poslednej metóde `navigator.geolocation.clearWatch()`. Prostredníctvom nej sa sledovanie ukončí.

##WebStorage

Táto technológia umožňuje webovým aplikáciám ukladať dáta priamo do klientského prehliadača. Podobnú funkčnosť sa dá dosiahnuť používaním Cookies.

Implementácia WebStorage má oproti Cookies niekoľko výhod:

- Cookies sa prenášajú pri každej požiadavke na server - zvyšuje sa tým množstvo prenesených dát.
- V Cookies sa nešifrovane môžu prenášať súkromné údaje (Ak sa nepoužíva šifrovanie komunikácie cez SSL).
- Cookies sú obmedzené približne na 4kB. Je to málo na rozsiahlejšie dáta, ale veľa na prenášanie pri každej požiadavke.
- Pri použití WebStorage dostaneme omnoho viac priestoru a dáta sa zakaždým neprenášajú.

V rámci špecifikácie sú dva typy úložišť podla perzistencie. Jeden typ je lokálny (ukladá dáta kým nie sú skriptom vymazané) a druhý reláciu (platí do zatvorenia prehliadača). Dôležitou vlastnosťou je, že úložišia patria doménam. Z toho vyplýva, že ak je webaplikácia otvorená vo viacerých taboch prehliadača súčasne, tak má každý tab prístup k aktuálnym dátam aj keď boli upravené iba v jednom.

Možným nedostatkom špecifikácie je neurčenie veľkosti poskytovaného priestoru. Nie je sa teda možné spoľahnúť na dostupnosť nejakého zaručeného množstva pamäte.

Úložište funguje ako asociatívne pole - `key value` databáza.[^webstorage-w3c][^webstorage-zdrojak][^webstorage-zdrojak2]

[^webstorage-w3c]: http://dev.w3.org/html5/webstorage/
[^webstorage-zdrojak]: http://www.zdrojak.cz/clanky/webdesigneruv-pruvodce-po-html5-webstorage/
[^webstorage-zdrojak2]: http://www.zdrojak.cz/clanky/minulost-soucasnost-a-budoucnost-lokalniho-uloziste-pro-html5-aplikace/

>Feross Aboukhadijeh našiel spôsob[^6] ako zaplniť harddisk návštevníka ukladaním malého množstva dát pre množstvo subdomén. Takto je možné zaplniť návštevníkovi celý harddisk.

[^6]: [feross.org/fill-disk/](http://feross.org/fill-disk/)

##WebWorkers

Prostredníctvom WebWorkers delegujeme časť JavaScriptového kódu do zvlášť vlákna. Toto je veľmi výhodné pre zložité výpočty na hardvéri s viacjadrovým procesorom. Následne stačí prevziať hotový výpočet.[^webworkers-zdrojak]

[^webworkers-zdrojak]: http://www.zdrojak.cz/clanky/webdesigneruv-pruvodce-po-html5-multithreading-s-webworkers/

##WebSockets

WebSockets umožňuje zjednodušiť real-time komunikáciu medzi prehliadačom a serverom. O niečo podobné sa snaží napríklad AJAX pri ktorom sa môže v pravidelných intervaloch pýtať prehliadač servera na nový obsah.

V prehliadači s podporou WebSockets je dostupný rovnomenný JavaScriptový objekt. Pomocou neho je možné vytvoriť trvalé spojenie so serverom. Takto vytvorené spojenie je schopné čakať na správu od servera. V prípade že má server dáta ktoré je potrebné dodať používateľovi, server ich odošle a klient prijme.[^websockets-zdrojak][^websockets-w3c]

[^websockets-zdrojak]: http://www.zdrojak.cz/clanky/web-sockets/
[^websockets-w3c]: http://dev.w3.org/html5/websockets/

##Multimédia

HTML5 prinieslo množstvo noviniek v použití multimédií na internete. Vďaka novinkám už nie je potrebné používať doplnky tretích strán.

###Video & audio

Na prehrávanie videa a zvuku vo webaplikáciach nie sú so špecifikáciou HTML5 potrebné pluginy tretích strán. Najväčším zostávajúcim problémom je roztrieštenosť podpory kodekov multimediálnych súborov. Špecifikácia neurčuje použitý kodek a teda sa jednotlivý výrobcovia prehliadačov rozhodovali podla vlastných preferencií. Firefox a Chrome podporovali už v minulosti otvorený kodek Ogg/Theora a Googlom vyvinutý kodek WebM/VP8. Napriek prvotnému odmietaniu podpori patentami chráneného kodeku MPEG-4/H.264 Mozillou, je aj tento kodek už dve verzie podporovaný. Jediným bežne používaným prehliadačom nepodporujúcim tento kodek je Opera. Tá podporuje iba WebM/VP8 a Ogg/Theora.

Zatiaľ nie je možné poskytnúť používateľom obsah v jednom kodeku, ale je nutné ukladať súbory na serveroch aspoň v dvoch formátoch.[^video-audio]

[^video-audio]: http://caniuse.com/#feat=video

###Kamera & mikrofón

V rámci štandardu [Media Capture and Streams](http://www.w3.org/TR/mediacapture-streams/) je definované JavaScriptové API pre prístup k zachytávaniu obrazu a zvuku z hardvéru klienta webaplikáciou. Takto zachytené dáta je možné použiť v aplikácií alebo streamovať.[^kamera-mikrofon]

[^kamera-mikrofon]: http://www.w3.org/TR/mediacapture-streams/

###Titulky

Vzhľadom na štandardizáciu videa bola logickým dôsledkom aj snaha o štandardizovanie textových súborov k videám - titulkov. Vzhľadom na podobnosť a jednoduchosť jednotlivých tituľkových súborov nie je problém používať v prostredí internetu prakticky akýkoľvek. Problém nastáva ak chceme podporovať iba jeden univerzálny. Výsledkom snaženia skupipny W3C je titulkový formát [WebVTT (Web Video Text Tracks)](http://dev.w3.org/html5/webvtt/).

Titulky nesú okrem informácie o časovaní a texte aj sémantický obsah (meno hovoriaceho) a nastavenie rôznych vlastností ako napríklad veľkosti zobrazenia. K titulkom je možné pristupovať pomocou DOM a meniť ich zobrazenie napríklad použitím CSS.[^titulky]

[^titulky]: http://dev.w3.org/html5/webvtt/

##Vykresľovanie

Dôležitými novinkami HTML5 sú vylepšenia prípadne nové vlastnosti vo vykresľovaní.

###Canvas

Canvas je vlastne rastrové *plátno* na ktoré je možné kresliť prostredníctvom JavaScriptového API. Je možné kresliť jednoduché grafické prvky a z nich skladať zložitejšie. Možnosti použitia tejto technológie sú obmedzené iba kreativitou.

###WebGL

Štandard WebGL[^webgl] rozširuje možnosti canvasu. Je založený na OpenGL ES 2.0 Umožňuje vykresľovať priamo v prehliadači interaktívnu 3D grafiku za použitia jednotného rozhrania. Nespornou výhodou je využitie potenciálu grafickej karty.[^webgl-specs]

[^webgl]: Web-based Graphics Library
[^webgl-specs]: https://www.khronos.org/registry/webgl/specs/1.0/

#Desktopové aplikácie

V posledných mesiacoch, je čoraz viac populárne programovanie desktopových aplikácií v HTML5. Viditeľná je snaha poskytovateľov operačných systémov umožniť programovať aplikácie čo najširšiemu spektru programátorov. Tým si zabezpečia dostatok softvéru pre používateľov a konkurenčnú výhodu.

##Windows 8

V poslednej verzií operačného systému od Microsoftu je možné pristupovať k jednotnému *Windows Runtime* na všetkých zariadeniach cez jedno JavaScriptové API. Takto vytvorené aplikácie je možné distribuovať prostredníctvom Windows Store.

##Ubuntu

Od verzie Ubuntu 12.10 je možné vo webaplikáciách inicializovať špecializované JavaScriptové API pre komunikáciu s operačným systémom. Pomocou objektu `Unity` môžu webaplikácie používať notifikácie systému, ovládanie media playeru, Unity HUD, applet správ a spúšťač aplikácií.[^unity]

[^unity]: http://developer.ubuntu.com/api/ubuntu-12.04/javascript/

##FirefoxOS

Samostatnou kategóriou je novinka na trhu - mobilný systém FirefoxOS. Prvé zariadenia sa dostali do predaja len pred pár dňami. Hlavným lákadlom má byť extra jednoduchá tvorba aplikácií. Všetky aplikácie vo FirefoxOS sú tvorené výhradne pomocou technológií HTML5. To znamená, že na prístup ku všetkému hardvéru a softvéru je používané výhradne JavaScriptové API. Až najbližšie roky preveria či je vízia systému s čisto HTML5 aplikáciami tá správna.[^firefoxos]

[^firefoxos]: http://www.zdrojak.cz/clanky/webapi-firefox-os/

**Prehľad dostupných API:**

- základné
	- Vibration API
	- Screen Orientation
	- Geolocation API
	- Mouse Lock API
	- Open WebApps
	- Network Information API
	- Battery Status API
	- Alarm API
	- Web Activities
	- Push Notifications API
	- WebFM API
	- WebPayment
	- IndexedDB
	- Ambient light sensor
	- Proximity sensor
	- Notification
	- FMRadio
- privilegované
	- Device Storage API
	- Browser API
	- TCP Socket API
	- Contacts API
	- systemXHR
- certifikované
	- WebTelephony
	- WebSMS
	- Idle API
	- Settings API
	- Power Management API
	- Mobile Connection API
	- WiFi Information API
	- WebBluetooth
	- Permissions API
	- Network Stats API
	- Camera API
	- Time/Clock API
	- Attention screen
	- Voicemail

#Záver

Do tohoto prehľadu by si určite zaslúžili zaradiť aj ďalšie časti HTML5 ako napríklad `CSS3`, `Multitouch`, `WebRTC`, `FileAPI`, `Drag&Drop` a iné. Z dôvodu rozsahu to ale nie je možné pretože by to bez problémov vystačilo na knihu. Cieľom dokumentu bolo predstaviť hlavné novinky ktoré HTML5 prináša. Vývoj tohoto IT segmentu prebieha veľmi búrlivo, napriek tomu sú zjavné nemalé snahy o otvorenú štandardizáciu a spoluprácu väčšiny zúčastnených. Viditeľným je zmenený prístup spoločnosti Microsoft. V minulosti bola známa vytváraním vlastných uzatvorených štandardov. Dnes sa bráni implementácií niektorých častí špecifikácií do svojich produktov, kým nebudú definitívne uzatvorené. Týmto spomaľuje prenikanie nových technológií medzi širokú verejnosť.

Je nepopierateľné, že HTML5 predstavuje obrovský skok vopred. Oproti webu známemu pred rokmi, je aktuálne v situácií kde môžu vývojári a používatelia fungovať bez doplnkov tretích strán. Jednoduchá a bezpečná implementácia moderných funkcionalít je budúcnosťou.

Žiaľ reálne nepoužívajú všetci používatelia aktualizované prehliadače a teda je vo väčšine prípadov nutná spätná podpora prostredníctvom starších technológií. Toto je najväčšou brzdou rozvoja a podpory nových technológií. Vzhľadom na to, že HTML5 *iba* zjednodušuje a zabezpečuje implementáciu rôznych techník existujúcich aj pred HTML5, je vytváranie takýchto aplikácií určitým nadštandardom. Nie každý si môže dovoliť robiť moderné aplikácie ktoré sú v konečnom dôsledku iba nadstavbami už fungujúcich.

Možnosti na vytváranie moderných webaplikácií tu reálne sú. Najväčším obmedzením je vlastná kreativita a schopnosť účelne ich využiť.