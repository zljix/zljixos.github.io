# Orbit OS 0.12.0

Aplikacija na hrvatskom za samostalno učenje strukture, funkcija i mehanizama operacijskih sustava. Radi u pregledniku, bez računa i aplikacijskog poslužitelja. Ovo je nastavak projekta iz `zljix/zljix.github.io`, sada u repozitoriju `zljix/zljixos.github.io`. GitHub Pages adresa projekta je https://zljix.github.io/zljixos.github.io/ nakon uključivanja Pagesa.

## Vođeno učenje i igrifikacija

**Uči od početka** vodi kroz osam misija: dijelovi računala, uloga OS-a, procesi, CPU, memorija, čitanje datoteke, dretve i zastoj. Svaka povezuje ranije znanje, cilj, jednostavne definicije, čestu zabludu, riješeni primjer, promjenu uvjeta pokusa i primjenu na novi slučaj.

Osnova svake misije donosi **100 XP**: kratka provjera 10, redoslijed 20, usporedba uvjeta 20, dvije provjere po 10 i samostalna primjena 30. Za usporedbu treba proći sve uvjete (dva ili tri). Predviđanja se ne kažnjavaju. Zadnji zadatak traži i ishod i razlog.

**Easy** (100 XP po misiji) vodi početnika kroz dva izbora i početak redoslijeda. **Moderate** (120 XP) dodaje primjenu u novoj situaciji. **Hard** (140 XP) dodaje dijagnozu s tri povezane odluke i pomoć nakon prvog pokušaja. Težinu možeš promijeniti bez gubitka ili udvostručavanja bodova.

| Aktivnost | Najviše XP |
| --- | ---: |
| Osam misija s dodatnim primjenama i dijagnozama | 1120 |
| Jedanaest praktičnih laboratorija | 220 |
| Četrnaest uvjeta detaljnih mehanizama | 140 |
| Sedam mrežnih izazova | 140 |
| Završni izazov — najbolji rezultat | 100 |
| DOS/CMD i Linux Shell — 12 razina | 1200 |
| **Ukupno** | **2920** |

Pet rangova i devet znački prate postignuća. Pogreška otvara objašnjenje, pomoć i ponavljanje. Svaki zadatak boduje se jednom; ponavljanje ne gomila XP. Posebno se čuvaju prvi odgovor, zadnji odgovor, njihove težine, broj pokušaja i pomoć. Easy sadrži ugrađeno vođenje. Bodovi su uvijek vidljivi u gornjoj traci, u svim aplikacijama. Mrežne dijagnoze nisu uključene u statistiku prvih odgovora.

Nakon osam misija dovršenih na odabranoj težini otključava se završni izazov: deset pitanja, bez pomoći i povratne informacije o točnosti do predaje. Nakon predaje slijede rezultat, objašnjenja i plan ponavljanja. Svaka težina ima vlastitu banku i dvije inačice pitanja po temi. Već započeti pokušaj zadržava izvornu težinu. Najbolji rezultati prikazuju se po težinama, a u ukupni XP ulazi jedan najbolji rezultat. Čuva se najviše 20 pokušaja, uključujući najbolji za svaku težinu i najnoviji. Nema vremenskog ograničenja.

Sve radnje i strukturirani odgovori boduju se automatski, bez nastavničke intervencije. Stare slobodne bilješke ostaju arhivirane; ne pretvaraju se automatski u dokaz znanja. XP je napredak u učenju uz dostupnu pomoć, a ne školska ocjena niti zaštićen ispitni zapis.

## DOS/CMD i Linux Shell

Aplikacija **DOS/CMD i Linux** dostupna je iz pregleda misija, izbornika aplikacija i prečaca na radnoj površini. Dodaje **12 razina i 60 praktičnih zadataka**. Učenik upisuje naredbe, vidi izlaz i promjene virtualnog prostora, a model provjerava cilj nakon svake naredbe.

| Razina | DOS/CMD | Linux Shell |
| --- | --- | --- |
| 1 | `dir`, `cd`, `type`, relativne/apsolutne putanje | `pwd`, `ls`, `cd`, `cat`, putanje |
| 2 | `mkdir`, `echo`, `>`, `>>`, navodnici | `mkdir`, `echo`, `>`, `>>`, navodnici |
| 3 | `copy`, `ren`, `move` | `cp`, `mv` |
| 4 | `find`, `/i`, cjevovodi i izvještaj | `grep -F`, `-i`, cjevovodi i izvještaj |
| 5 | `del`, `rd`, čuvanje važne datoteke | `chmod`, `ls -l`, čitanje i pisanje vlasnika |
| 6 | Priprema predaje, izvještaj, arhiviranje i čišćenje | Priprema predaje, izvještaj, arhiviranje, `rm` i `rmdir` |

Svaka razina uvodi pojmove i primjere prije rada. Easy obuhvaća 3 temeljna zadatka (60 XP), Moderate dodaje primjenu (80 XP), a Hard povezani izazov (100 XP). Svaki zadatak vrijedi 20 XP samo jednom. Easy prikazuje mogući postupak; na Moderate pomoć je na zahtjev; Hard otvara pomoć nakon pokušaja. Sljedeća razina putanje otključava se nakon prva tri zadatka prethodne. Obje putanje mogu se započeti neovisno.

Provjerava se stvarni rezultat i, gdje je potrebno, izvedena radnja. Ekvivalentne putanje i podržani sinonimi naredbi vrijede. Ponavljanje vraća virtualne datoteke razine, ali čuva bodove i evidenciju. Svaka razina ima vlastite datoteke; ne dira ostale datoteke igre ni računala. DOS/CMD je ograničeni model Windowsova cmd.exe s naredbama koje dijelom potječu iz DOS-a; nije puni MS-DOS ni PowerShell. Linux model nije potpuni Bash. Ne izvršava skripte, programe, mrežne radnje ni sistemske pozive. Granice modela navedene su u vježbi.

## Spremanje i offline rad

- Napredak, bodovi, pokušaji i datoteke spremaju se lokalno. **Moj rad** omogućuje JSON kopiju za prijenos na drugi uređaj.
- Verzija 0.12 pri prvom otvaranju kopira lokalni rad 0.11 ako postoji u istom pregledniku, a zatim ga čuva zasebno. Otvaranje stare aplikacije zato ne prepisuje nove terminalske rezultate. Prijenos između preglednika i uređaja ide JSON kopijom.
- Nadogradnja čuva stare datoteke, pokuse, osvrte i nedovršene nacrte. Novi zadatci imaju zaseban zapis bodovanja.
- Za prvo otvaranje na mobitelu potreban je internet. Ikona preuzimanja je siva i onemogućena dok cijeli paket nije spreman. Zatim postaje zelena i otvara **Spremi za offline rad**: preuzimanje samostalnog HTML-a, dodavanje na uređaj kad je podržano i upute za početni zaslon. HTML datoteka također je predmemorirana pa se može preuzeti bez veze.
- Poslije nadogradnje zatvori sve kartice/prozore Orbita i ponovno otvori aplikaciju; nova offline verzija ne zamjenjuje aktivnu lekciju usred rada.
- Za računalo preuzmi [Orbit-OS.html](downloads/Orbit-OS.html) i otvori ga preglednikom bez lokalnog poslužitelja. Rad prenosi zasebnom JSON kopijom.
- **Izvještaj** prikazuje automatske bodove, odgovore, pokušaje i potvrđene radnje. Može se kopirati, ispisati ili izvesti; nikome se ne šalje automatski.

## Razvoj i objava

Izvorni kod, testovi i skripte su u `source/`. Uz Node.js i npm:

```sh
npm install
npm test
npm run build
npm run check:artifact
```

Izgradnja stvara `dist/Orbit-OS.html` i mobilni paket u `dist/mobitel/`, uključujući `downloads/Orbit-OS.html`. GitHub Pages koristi `main`, mapu `/`; mobilne datoteke objavljuju se u korijenu, a desktop HTML u `downloads/`. Ne objavljuju se QA datoteke, učenički radovi ni `node_modules`.

Verzija 0.12.0 ima 103 automatizirana testa, uključujući svih 60 terminalskih ciljeva, oba dijalekta, dozvole, ponavljanje, prijenos i migraciju. Provjereni su prijelaz prve misije kroz 100/120/140 XP, pomoć na Hard, trajna traka bodova, očuvanje težine i ranijih rezultata, početnička misija do 100 XP, ispravci, nastavak nakon osvježavanja, oba završna pokušaja, praktični zaključak, detaljni mehanizam, mrežna dijagnostika i širine 320, 375 i 414 px u Chromiumu. Test na fizičkim iPhone/Android uređajima ni evaluacija s razredom nisu provedeni.


Provjera 0.12 u Chromiumu 134: stvaran unos pogrešne naredbe i ispravka, 60 → 80 → 100 XP, nastavak nakon osvježavanja, Linux odbijen zapis i naknadna promjena dozvole, pomoć na Hard, ukupni bodovi uvijek na vrhu, širine 320/375/414 px bez vodoravnog prelijevanja, ponovno otvaranje bez mreže i preuzimanje pripremljenog HTML-a bez mreže. Preuzeti samostalni HTML otvara se i pokreće nove razine. Nema zabilježenih JavaScript pogrešaka. Fizički iPhone/Android i Safari nisu testirani.

Za prvo uključivanje web-adrese novog repozitorija: **Settings → Pages → Deploy from a branch → main → /(root) → Save**. Naziv repozitorija ne stvara zasebnu adresu `zljixos.github.io`: uz vlasnika `zljix` riječ je o projektnoj adresi `zljix.github.io/zljixos.github.io/`.
