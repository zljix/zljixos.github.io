# Orbit OS 0.12.0 — razvoj

Samostalni desktop HTML i mobilni PWA nastaju iz `public/orbit/` pomoću `scripts/build.mjs` i esbuilda 0.28.0. Nema aplikacijskog poslužitelja niti udaljenog bodovanja.

## Moduli i kompatibilnost

- `course-data.js`: osam lekcija, primjeri i 18 uvjeta pokusa.
- `course-model.js`: zadržan format navigacije i povijesnih odgovora verzije 0.9. Stari kriterij `finished` ostaje samo radi čitanja prethodnog zapisa; novo dovršavanje izvodi se iz bodovanih zadataka.
- `game-data.js`: 103 objektivna zadatka (48 osnovnih misija, 16 dodatnih slučajeva, 11 laboratorija, 28 mehanizama); osnovna banka završnog izazova za Moderate. Pravilne opcije imaju stabilne kanonske indekse.
- `difficulty-data.js`: tri putanje (100/120/140 XP), 16 primjena i dijagnoza, Easy i Hard završne banke. Ukupno 60 završnih pitanja s kanonskim indeksima.
- `game-model.js`: validacija, preduvjeti, evidencija aktivnosti, prvi/zadnji odgovor, pomoć, XP, rangovi, značke, završni pokušaji i izvještaj.
- `game-ui.js`: zajednički obrasci izbora, redoslijeda i para ishod–razlog. Opcije se deterministički miješaju samo u prikazu.
- `game.css`, `course.js`: mapa misija, četiri faze učenja, povratna informacija, ponavljanje, završni izazov i prilagodba mobitelu.
- `network-model.js`: objektivna dijagnoza uz provjerene pokuse; stari tekst ostaje arhiviran i pri ponovnom rješavanju.
- `teaching.js`, `explorer.js`: postojeći laboratoriji i mehanizmi koriste isto automatsko bodovanje.

`learning.game` je aditivno proširenje radnog prostora. Odsutno polje inicijalizira prazne rezultate i čuva kopiju ranijih nacrta mehanizama u `legacy`. Datoteke, stare lekcije, bilješke, mrežni zapisi i spremljene verzije zadržavaju se. U 0.11 dodani su `difficulty`, `firstMode`, `lastMode` i težina svakog završnog pokušaja. Postojeći zapisi bez težine pokazuju Easy putanju radi očuvanja dovršenih misija; stari odgovori i završni ključevi ostaju Moderate, prema izvornom bodovanju. Lokalni ključ 0.12 je `orbit-os.offline.workspace.v1.shell12`. Pri prvom otvaranju kopira se čitljiv raniji zapis `orbit-os.offline.workspace.v1`; stari zapis ne mijenja se. Odvojeni ključ sprječava da stara aplikacija na istom originu odbaci nova polja.

`FileSystem.transact()` validira stanje, dopunjuje dokaze aktivnosti, sprema i vraća prethodno stanje ako operacija ne uspije. Milestones su monotoni; nova inačica pokusa ne briše ranije potvrđenu aktivnost. XP i značke računaju se iz provjerenih oblika odgovora i evidencija; uvezeni proizvoljni zbroj XP-a se ignorira. To nije zaštita od izmjene klijentskog koda ili smisleno krivotvorenog lokalnog zapisa.

Završna provjera sprema kanonske odgovore i broj pokušaja. Nepotpun pokušaj nema rezultat. Ukupni XP uzima najbolji rezultat, a povijest je ograničena na 20, uz očuvanje najboljeg za svaku težinu i najnovijeg. Prikaz aktivnog pokušaja ne otkriva ključ ni točnost. Promjena težine ne mijenja njegovu banku. U ukupne bodove ulazi najbolji rezultat preko svih težina, uz zaseban prikaz najboljeg po težini.

## Provjere

```sh
npm install
npm test
npm run build
npm run check:artifact
```

103 testa pokrivaju postojeće modele, postupke oporavka, migraciju, ograničenja bodovanja, sve kategorije do 2920 XP, neponavljanje bodova, sve uvjete usporedbe, pogrešne i nepotpune odgovore, čuvanje pomoći i prvog odgovora, završne pokušaje, ograničenje povijesti, uvoz/izvoz i očuvanje ranijih mrežnih bilježaka. Provjera artefakta traži jednu valjanu ugrađenu skriptu, ugrađene stilove, desktop bez mrežnih API poziva, valjan manifest i offline worker.

Ranija UI provjera u Chromiumu: misija do 100 XP s pogreškom i ispravkom; nastavak nakon osvježavanja; završni rezultati 40/100 i 100/100 s obnovom aktivnog pokušaja; laboratorijski zaključak; svih sedam koraka jednog detaljnog mehanizma; mrežni DNS izazov prije/poslije popravka; širine 320, 375 i 414 px. Provjera 0.11: prva misija 100 → 120 → 140 XP, pogrešna Hard dijagnoza, pomoć i ispravak; promjena težine bez gubitka XP-a i ponovno otvaranje; trajna traka i prikaz 320/375/414 px. Fizički iPhone/Android i rad s razredom nisu testirani.

## Objava

Korijen GitHub repozitorija sadrži šest mobilnih datoteka. Desktop HTML je u `downloads/`, izvor u `source/`. Ne objavljuj učeničke JSON kopije, testne radne prostore, QA HTML ni `node_modules`.

Worker provjerava šest predmemoriranih resursa: mobilni HTML, manifest, tri ikone i `downloads/Orbit-OS.html`. Spremnost ikone zahtijeva potvrđene `ready` i `downloadReady` te uspješno pripremljen neprazan HTML Blob. Eksplicitni `fetch` prolazi kroz worker i preuzima datoteku u memoriju prije zelene ikone; klik sprema Blob bez novog mrežnog zahtjeva. To pokriva preglednike čije nativno preuzimanje ne prolazi kroz worker; ikona je inače onemogućena. Stari worker ne može pogrešno potvrditi novi paket. Gumb otvara dijalog s HTML preuzimanjem, instalacijom kad preglednik nudi događaj i uputama za mobilne preglednike. Desktop preuzimanje radi i iz offline predmemorije. Worker dobiva oznaku iz verzije i hashiranog sadržaja oba HTML-a, manifesta, workera i ikona. Nova predmemorija instalira se cjelovito, bez brisanja stare pri pogrešci. Ne koristi `skipWaiting`; nadogradnja čeka zatvaranje prethodnih prozora aplikacije. Učenički podatci u localStorage odvojeni su od predmemorije aplikacije.

## Razina naredbenog retka (0.12)

- `shell-engine.js`: ograničeni interpreter CMD/Linux, putanje, tekstualni datotečni sustav, cjevovodi i izlaz; bez `eval`, pokretanja procesa ili mrežnih poziva.
- `shell-data.js`: 12 razina, pojmovi, primjeri, 60 provjerljivih ciljeva i jedna moguća rješenja za pomoć.
- `shell-model.js`: zapis naredbi, težine, pomoći i ponavljanja. Radni prostor, tijek, osvojeni zadatci i XP rekonstruiraju se izvršavanjem tog zapisa. Uvezeni XP i oznake dovršenosti ignoriraju se. To nije zaštita od namjernog krivotvorenja valjanog zapisa ili izmjene klijentskog koda.
- `shell-ui.js`, `shell.css`: dvije putanje, uvod prije terminala, mobilne tipke za posebne znakove i vidljiv cilj. Novi zapis `learning.shell` je aditivan; stari radni prostori dobivaju prazne terminalske rezultate.
- `test/shell.test.js`: 12 smislenih testova interpretera, svih ciljeva, težina, pomoći, migracije, alternativnih rješenja, ograničenja i ukupnog bodovanja.

Tri/četiri/pet zadataka znače 60/80/100 XP. Osvojeni zadatak ostaje označen pri ponavljanju; trenutni prolaz ponovno kreće od prvog. Nova kategorija dodaje 1200 XP, pa ukupni maksimum igre postaje 2920 XP. Nove značke zahtijevaju svih 600 XP odgovarajućeg dijalekta. Svaka razina sprema najviše 400 radnji; nastavni disk ima najviše 80 stavki, datoteka 8000 znakova, naredba 400 znakova. Koristi se ograničen predmemorirani rezultat rekonstrukcije za svaku razinu.

Svjesna pojednostavnjenja: nema zamjenskih znakova, varijabli, ekspanzija, skripti, simboličkih poveznica, pokretanja programa ili mreže. Linux provjerava vlasnikovo čitanje/pisanje obične datoteke; ne modelira potpunu hijerarhiju prava direktorija i ACL. Nepodržana ili neuspjela naredba atomarno vraća stanje; stvarni shell može imati djelomične učinke. Na to se učenika upozorava u samoj vježbi. CMD `find` pri izravnom čitanju daje zaglavlje; u zadatcima za čisti izvještaj koristi se `type | find`.

Provjereni primarni izvori za ponašanje naredbi:
- https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/cmd
- https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/dir
- https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/find
- https://www.gnu.org/software/bash/manual/html_node/Pipelines.html
- https://www.gnu.org/software/bash/manual/html_node/Redirections.html
- https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html

Provjera sučelja 0.12: Chromium 134, desktop 1365×950 i mobilni prikazi 320/375/414×850. Provjereni su pogrešan unos, sve težine prve CMD razine, povrat nakon osvježavanja, Linux 400 → odbijen zapis → 600 → uspješan zapis, pomoć na Hard i odsutnost vodoravnog prelijevanja. Provjerena je instalacija workera pod projektom `/zljixos.github.io/`, ponovno otvaranje bez mreže, preuzimanje pripremljenog Bloba i pokretanje samostalnog HTML-a. Nema JavaScript runtime pogrešaka. Fizički uređaji i Safari nisu testirani.
