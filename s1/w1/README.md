U sklopu prve nedelje rada na projektu nam je cilj da svaki student postane familijaran sa osnovnim tehnologijama u kojim će graditi projekat. Da bismo postigli prethodni cilj, definišemo zadatak koji svako od vas treba samostalno da uradi. Ispunjenje ovog cilja će stvoriti temelje potrebno da se svi kasniji zadaci na projektu realizuju, zbog čega smo izradili i u okviru ovog direktorijuma sabrali materijale koji će vam pomoći da rešiš zadatak.

# Razvoj proste funkcionalnosti
Na početku svakog sprinta je potrebno dogovoriti u okviru tima ko će koji zadatak da rešava. U prvoj nedelji se fokusiramo na razvoj funkcionalnosti u početnom ASP.NET i Angular projektu. Zadatak podrazumeva sledeće korake:

1. Sređivanje kartice koja definiše zadatak.
2. Izrada koda za serversku (backend) aplikaciju.
3. Izrada koda za klijentsku (frontend) aplikaciju.
4. Otvaranje i dokumentovanje *pull request*a.
5. Prepuštanje kolegi da revidira novi kod i odgovaranje na komentare.
6. Zatvaranje *pull request*a.

Preporuka je da prvi korak rešiš što pre, jer uključuje planiranje rešavanje ostatka posla.
<br/><br/><br/><br/>
## 1. Sređivanje kartice koja definiše zadatak
Rešavanje zadatka kreće na Trello tabli, gde je potrebno da uradiš sledeće:

<ol type="a">
  <li>Kartica treba da bude dodljena tebi (Klik na karticu, Members -> Izaberi svoje ime).</li>
  <li>Rok za rešavanje kartice je postavljen do sledećih vežbi (Klik na karticu, Dates -> Odaberi datum).</li>
  <li>Kartica je postavljena u "In Progress" listu kartica.</li>
  <li>U tvom kalendaru je definisano vreme za rešavanje kartice (više detalja ispod).</li>
  <li>Tekst kartice je ispravno definisan (više detalja ispod).</li>
</ol>

### d. Planiranje rada na kartici
Teško nam je da kažemo koliko vremena će ti biti potrebno da rešiš karticu jer zavisi od veštine sa kojom ulaziš u ovu priču. Ipak, verujemo da će većina uspeti da reši kompletan zadatak za 5 sati, a deo i brže. Obrati pažnju da je karticu potrebno kompletno rešiti do sledećih vežbi. Ovo uključuje i 5. korak - reviziju koda od strane kolege i rešavanje problema.

Prilikom planiranja treba da uzmemo u obzir potrebno vreme (do 5 sati) i zavisnosti koje postoje sa ostalim članovima tima (u ovom slučaju revizija koda i rešavanje revizije). Spram ovih zadataka je naša preporuka da:

- Rezervišeš slot u kalendaru od 4 sata nekad u naredna 4 dana. Tokom ovog slota ti je cilj da rešiš korake 2, 3 i 4. Ako si nesiguran u svoje veštine, bolje je da ova 4 sata rezervišeš ranije u tom opsegu kako bi tražio pomoć ako ti bude potrebna.
- Ostaviš kolegi i sebi bar 2 dana da se uradi revizija i da stigneš u okviru od 1 sat da odgovoriš na komentare, dobiješ potvrdu da je sve ok i zatvoriš *pull request* (korak 6) dan pred vežbe.
- Bitno je da ostane taj 1 dan da se reše bilo kakvi konflikti koji će se pojaviti kod deljenih datoteka.

### e. Sređivanje teksta korisničke priče
Svaka kartica predstavlja korisničku priču koja definiše želju koju korisnik ima za softver. Predstavlja značajno prostiji oblik slučaja korišćenja, gde **<a src="https://www.youtube.com/watch?v=RV6gnFKJY9U" target="_blank">[sledeći video]</a>** ističe njenu tipičnu strukturu (slobodno gledaj na x2).

Potrebno je da:

- Definišeš naslov korisničke priče prateći connextra šablon (As a... I want... So that...) istaknut u prethodnom videu.
   - Najveći problem će ti predstavljati "So that" deo priče, gde je potrebno da istakneš korist koju korisnik dobija od funkcionalnosti.
   - Izbegavaj da ponoviš "I want" deo teksta u "So that" sekciji, odnosno nemoj samo da preformulišeš drugi deo u trećem delu.
   - Pored guglanja, sledeći upit na GPTu će ti pomoći da bolje razumeš ovaj deo "_I am having trouble with understanding what to write in the "So that <benefit>" part of a user story_". Napiši GPTu šta ti je "As a" i "I want" deo i istakni šta misliš da je "So that" deo i zašto to misliš. Kroz tu interakciju ćeš utvrditi svoje razumevanje ove celine.
- U detaljima kartice su zabeležene dodatni podaci (*acceptance criteria*) za zadatak. U prvoj nedelji će se tekst svesti na pobrajanje polja koje entitet koji implementiramo treba da ima.
<br/><br/><br/><br/>
## 2. Izrada koda za serversku (backend) aplikaciju.
Materijali za podršku ovog koraka su definisani u **<a href="https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/back-end.md" target="_blank">zasebnoj stranici</a>**.
<br/><br/><br/><br/>
## 3. Izrada koda za klijentsku (frontend) aplikaciju.
Materijali za podršku ovog koraka su definisani u **<a href="https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/front-end.md" target="_blank">zasebnoj stranici</a>**.
<br/><br/><br/><br/>
## 4. Otvori i dokumentuj PR-ove.
U momentu kada je razvoj spreman za reviziju (rešenje se builda, testovi prolaze, funkcionalnost je implementirana) potrebno je da otvoriš PR na repozitorijumu za back-end i za front-end. Kako se otvara PR možeš proučiti **<a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request" target="_blank">ovde</a>**. Bitno je istaći da otvaramo PR gde hoćemo tvoju *feature granu* da spustimo na *development*.

Uz otvaranje PRa je neophodno navesti prateću dokumentaciju u opis PRa:

- Za back-end PR treba istaći (možeš kopirati teze ispod i popuniti ih u PR opisu):
  - **Change goal**: Tekst korisničke priče ili link na karticu.
  - **Database change**: Spisak izmena koje će zahtevati izmenu baze (npr. dodavanje nove tabele, uklanjanje ili dodavanje polja u entitetima koja se mapiraj na kolone tabele).
- Za front-end PR treba istaći:
  - **Change goal**: Tekst korisničke priče ili link na karticu.
  - **UI changes**: Skup screenshotova koji ističu najbitnije izmene na korisničkom interfejsu (za prvu nedelju screenshot tabele i screenshot forme je dovoljan).

Dokumentovanje navedenih informacija će kolegi olakšati reviziju koda, a tebi će pomoći da razviješ korisnu naviku.
<br/><br/><br/><br/>
## 5. Zatraži reviziju koda i odgovori na komentare.
Kada je PR napravljen, moguće je zatražiti reviziju putem *Reviewers* sekcije. Dogovori se sa timom ko će čije PRove da revidira. Na Trellu, prebaci svoju karticu u _Review_ sekciju.

Kada budeš sam radio reviziju kolegi, potrudi se da to uradiš u dogovoreno vreme i da ostaviš komentare koji će pokazati da si se udubio u proces. Smernice za izradu revizije se nalaze **<a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews" target="_blank">ovde</a>.

Tokom revizije koda obrati pažnju na:

- Narušavanje timske konvencije.
- Formatiranje i indentaciju koda.
- Nazive koji su korišteni u svim identifikatorima.
- Veličinu i složenost funkcija.
- Veličinu i složenost klasa.

Kada primetiš da su postojeće timske konvencije nedovoljno razrađene, zadatak ti je da javiš na deljenom četu (npr. putem Discorda) ostatku tima da postoji ova rupa u spisku konvencija vašeg tima.

Nakon što kolega ostavi komentare, potrebno je da odgovoriš na njih dodatnim ispravkama ili kroz diskusiju. Bitno je da ostane pisani trag vaše interakcije i ovo ćemo pratiti kako bismo se uverili da ste izgurali proces do kraja.
<br/><br/><br/><br/>
## 6. Zatvori PR.
Kolega treba da potvrdi da su ispravke adekvatne putem još jedne revizije. U tom momentu je PR prihvaćen i može se zatvoriti uz prebacivanje koda sa tvoje feature grane na development.

Ovom prilikom može nastati konflikt kod deljenih datoteka (npr. rutiranje u Angular aplikaciji, DbContext u .NET aplikaciji). Tom prilikom je neophodno rešiti konflikte, gde je preporuka da sigurniji studenti poslednji spajaju svoje grane sa developmentom kako bi rešili izazovnije konfliktne situacije.

Kada je PR zatvoren, prebaci svoju karticu u _Done_.
