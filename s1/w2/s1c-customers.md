Sav softver koji programiramo predstavlja nekakvo *rešenje*. Rešenje podrazumeva da postoji *problem* koji rešavamo. Excel koji sadrži stotine hiljada redova treba agregirati u neku bazu podataka. Ovo je problem. Python skripta koja čita dati Excel, primenjuje agregacionu funkciju i čuva rezultat u bazi podataka je moguće rešenje tog problema.

Ako pogrešno razumemo problem koji rešavamo, nije bitno koliko je kvalitetan naš kod ili upotrebljiv naš korisnički interfejs - pravimo rešenje za pogrešan problem, čime pravimo beskoristan softver. Sa druge strane, kada dobro razumemo problem nije toliko bitno koliko će kvalitetno biti naše rešenje - ako je u razumnoj meri upotrebljivo, biće korisno.

Pošto smo inženjeri, imamo tendenciju da prvo razmišljamo o rešenju pre nego što smo dobro razumeli problem. Formiramo preduzetničke ideje i vizije za naš proizvod tako što prvo zamišljamo sva svojstva našeg softverskog rešenja. Ovo je opasno jer u većini slučajeva (šacometrijski - 99.9%) ne razumemo problem i potrebe korisnika i možemo napraviti složeno softversko rešenje koje nije korisno.

Kroz kurs ćemo razgovarati sa krajnjim korisnicima u nekoliko navrata kako bismo razvili veštine za razumevanje problema koji korisnici imaju, što će nam pomoći da pravimo korisna rešenja.

# Definisanje persone

*Persona* predstavlja sliku našeg krajnjeg korisnika koju imamo na umu kad god pričamo o njihovim potrebama. Primere persona smo videli na uvodnim predavanjima (Ana, David, Vanja), a isto i kada smo istakli različite tipove studenata pre nekog vremena (Alisa, Bob, Džon).

Naše trenutne persone su izuzetno proste i svode se na ime (Ana, David, Vanja) i rolu (Autor, Turista, Administrator) koju imaju. Potrebno je da ih obogatimo detaljima koji će nam pomoći da razumemo perspektivu korisnika, njihove potrebe i probleme, spram kojih ćemo usmeriti razvoj našeg softverskog rešenja u kasnijim sprintovima. Ovo je posebno bitno za persone Autora i Turiste zbog kojih ćemo "dobijati pare", dok su Administratori "naši ljudi" (na početku smo to mi sami kao vlasnici softvera).

Da bismo produbili naše persone, potrebno je da:

1. Pronađemo ljude iz naše okoline koji su pogodni za intervju (bar jednog dobrog kandidata za Autora i bar dva dobra kandidata za Turiste).
2. Definišemo strukturu intervjua koji ćemo održati sa svakim korisnikom.
3. Sprovedemo intervju.
4. Analiziramo zapis intervjua i kreiramo mapu empatije za svaku personu.

## 1. Pronalazak pogodnih ljudi za intervju
Za prvi susret sa korisnikom je neophodno da pronađemo 4 osobe koje će 8 člana tima intervjuisati (svaku osobu 2 člana tima intervjuišu). Bitno je da imamo bar jednu osobu koju bismo intervjuisali kao Autora i bar dve kao turista (no ukupno treba 4 osobe, tako da 2+2 ili 1+3).

Svaki član tima treba da razmisli koga bi mogao od porodice i prijatelja da angažuje za ovu aktivnost. Tom prilikom treba uzeti u obzir sledeće faktore:

- Dostupnost osobe tokom semestra - Idealno biramo osobu koja će moći sa članovima tima da se sastane tri puta u toku semestra, svaki put po sat do dva.
- Kandidati za Turiste - Osobe koje ne putuju, koje uvek idu na istu lokaciju (npr. imaju kuću na moru) ili putuju sa idejom da budu ceo dan u bazenu ili banji nisu dobri kandidati za naše Turiste. Naši Turisti su ljudi koji vole na neki način da istražuju prostor (npr. hajk po prirodi, obilazak znamenitosti grada, upoznavanje lokalnih priča i legendi). Ne treba da isključimo ljude koji putuju sa porodicom. Iako njihove ture nisu nužno uzbudljive, ima prostora da se ovaj deo tržišta cilja (npr. zabavne ili obrazovne ture za decu).
- Kandidati za Autora - Autore ćemo teže pronaći. Idealni kandidati su ljudi koji rade u turističkim agencijama ili lokalni vodiči i njih možemo kontaktirati čak i ako ih ne poznajemo tako što ćemo posetiti agencije ili pretražiti GetYourGuide sajt za lokalne ture. Alternativa su nam ljudi koji su "sami sebi vodič", odnosno turisti koji pažljivo planiraju svoja putovanja tako da svašta obiđu. Dobar kandidat za ovakvog autora je bilo ko ko temeljno proučava Google Maps, TripAdvisor i slične sajtove kada putuje, kao i neko ko dokumentuje svoja putovanja (npr. putem članaka).

Preporuka je da kontaktirate što više ljudi u ovom koraku kako biste identifikovali ne samo 4 osobe za ovaj prvi krug intervjua, nego i dodatnih 4 koji će nam trebati u trećem i četvrtom sprintu. Iz navedenog spiska biramo najbolje kandidate za prvi krug, gde uzimamo u obzir sledeće prioritete:

- Izbor osoba koje se dosta razlikuju (npr. turista koji voli avanturu i porodičnog turistu, autora kog interesuje priroda i autora koji se bavi istorijom).
- Izbor osoba sa više iskustva.
- Izbor osoba sa kojima imamo najbliži odnos.

Sa spiskom osoba možemo da organizujemo sastanke od okvirno jedan sat u toku nedelje.

## 2. Definisanje strukture intervjua
Pitanja koja ćemo postaviti tokom intervjua zavise od našeg cilja. U ovoj fazi ne želimo da pritiskamo osobe koje ispitujemo sa rešenjima (već napravljenim ili zamišljenim), već se fokusiramo na razumevanje njihovog pogleda, iskustva, želja i potreba vezanih za turizam i poddomen koji se tiče turističkog istraživanja.

Generalno će intervju imati sledeće segmente:

<ol type="a">
  <li>Uvod - pozdravljamo osobu i potvrđujemo svrhu našeg intervjua (kao vežba za projektni zadatak i kao aktivnost da se razumeju potrebe). Vredi istaći osobi da ne postoje pogrešni odgovori, već da je iskren odgovor najbitniji.</li>
  <li>Početak - proveravamo da li smemo da snimamo intervju i pripremamo svesku da hvatamo beleške za glavna pitanja u Razradi.</li>
  <li>Razrada - postavljamo glavna pitanja (detalji ispod).</li>
  <li>Retrospektiva - sabiramo ključne tačke koje smo prošli u toku Razrade. Pitamo osobu da li bi nešto dopunila ili posebno naglasila od pređenog. Ako ima vremena, u ovom koraku možemo da pričamo o konkretnom softveru koji bismo pravili i kakve početne ideje imamo za njegov razvoj.</li>
  <li>Zaključak - zahvaljujemo se osobi za izdvojeno vreme i podeljena iskustva i priče. Proveravamo da li je u redu da za okvirno četiri nedelje organizujemo sledeće viđanje.</li>
</ol>

### c. Razrada pitanja za intervju
Najbitniji deo ovog zadatka je priprema dobrih pitanja za intervju. Intervju koji sprovodimo je takozvani _needfinding interview_, gde želimo da razumemo potrebe naših turista i autora. Vredi iskoristiti ovu ključnu reč i videti kako nam GPT može pomoći sa sledećim upitom (sličan upit možemo napraviti za autora):
```
I want to create a needfinding interview.

My customer segment includes tourists that enjoy exploring their travel destinations. These are not necessarily adventurers, just people that enjoy exploring nature, cities, history, culture, art, etc.

I want to create a solution that can help them explore in an engaging way.
```
U nastavku su neka pitanja koja nam mogu pomoći da razumemo korisnike (boldom su interesantnija pitanja):

- Koliko često putuju, na kakav tip destinacije i kakvu vrstu putovanja generalno vole? Ovim definišemo grube crte persone (da li je avanturista, porodični turista, istoričar...).
- Šta su bila omiljena putovanja u poslednjem periodu i zašto? Šta su bila bezveze putovanja i zašto? Konkretne priče sakrivaju puno interesantnih detalja koji nude ideje za funkcionalnosti.
- Na osnovu čega biraju destinacije? Koliko istražuju destinaciju pre putovanja? Koliko istražuju kada su tamo?
- Šta vole da otkrivaju kad odu negde? Šta istražuju? Hranu? Bučne ili tihe ćoškove? Divljinu ili civilizaciju?
- **Da li su nekad išli na organizovane ture? Kakvo im je bilo iskustvo?**
- **Šta im predstavlja najveće probleme koji ih sprečavaju da istražuju ili im čine to iskustvo nelagodnim?**
- **Da li koriste neke alate (npr. mape, sveske) ili aplikacije da pomognu sa organizacijom putovanja i istraživanja? Šta izvlače iz njih? Šta im se ne sviđa kod njih?**

Ako osoba prvi put priča o svojim putovanjima na ovaj način, verovatno će se uhvatiti konkretnih primera iz svog života (npr. "Prošle godine u Hrvatskoj je ovo baš bilo kul") umesto nekih opštijih zaključaka (npr. "Volim da obilazim staze koje su umereno fizički zahtevne, imaju raznoliki reljef i ne zahtevaju mnogo vraćanja istim putem"). Kod konkretnih priča, možemo da postavimo dodatna pitanja (npr. "Da li ste imali još neko iskustvo poput tog?", "Da li vam generalno prijaju iskustva sa ovim aspektom?") da pokušamo da uočimo širu temu.

## 3. Sprovođenje intervjua
Intervju je najbolje sprovesti u ambijentu koji nije previše bučan i gde se svi prisutni osećaju komforno. Preporuka je da ištampate strukturu intervjua i glavna pitanja koja hoćete da postavite da budu pri ruci.

Tokom intervjua jedan član tima može da vodi razgovor, dok će drugi biti posvećen zapisivanju interesantnih detalja. Ovo ne sprečava drugog člana tima da postavlja svoja pitanja.

Rezultat intervjua treba da bude snimak, zapisi ključnih tačaka (koje će se proći u Retrospektivi) i **fotografija sa osobom koja je intervjuisana** koju ćete priložiti asistentu na uvid.

## 4. Kreiranje mape empatije različitih persona
Za svaki sproveden intervju možemo da sastavimo jednu mapu empatije koju vezujemo za personu. Primer šablona za ovu mapu je naveden ispod:

![image](https://github.com/psw-ftn/supportive-information/assets/7092212/63f366f5-19cc-4b6d-a328-4332c530427b)

Koristeći datu sliku na draw.io alatu, možemo da popunimo praznine sa zapažanjima koje smo izvukli iz intervjua, po sledećoj strukturi:

- Šta misli i oseća (Think & Feel) - šta su unutrašnje misli, osećanja i stavovi osobe u vezi sa turističim istraživanjem ili turama?
- Šta vidi (See) - šta osoba primećuje tokom turističkog istraživanja ili tura? Roditelji će prvo gledati gde im se dete može povrediti, dok će mladi ispitivati šta su dobra mesta za izlaske.
- Šta čuje (Hear) - šta osoba čuje od bližnjih, zajednica kojim pripada, sajtova koje posećuje, turističkih agencija, itd. povodom turističkog istraživanja ili tura?
- Šta radi (Say & Do) - kako se osoba ponaša tokom turističkog istraživanja ili tura?
- Šta su izazovi (Pain) - šta mu smeta kod turističkog istraživanja ili tura? Šta mu smeta kod alata i aplikacija koje koristi? Šta su karakteristike negativnih iskustva koje je imao?
- Šta su želje (Gain) - šta osoba izvlači iz turističkog istraživanja ili tura? Šta mu se sviđa kod alata koje koristi? Šta su karakteristike pozitivnih iskustva koje je imao?

### Primer mape empatije za personu "Turista zaljubljen u kulturu"
Da ilustrujemo kako popuniti prethodno, u nastavku navodimo teze za personu "David - Turista zaljubljen u kulturu" (u tekstulanom obliku).

Think & Feel:

- Nestrpljiv da uroni u lokalnu kulturu i istoriju.
- Ceni autentična iskustva više od turističkih atrakcija.
- Želi da sazna o istorijskom značaju mesta.
- Brine se o poštovanju lokalnih običaja i bontona.

See:

- Istorijske spomenike, muzeje i galerije.
- Kulturne manifestacije i festivale.
- Lokalne zanatlije kako praktikuju tradicionalne veštine.
- Drevnu arhitekturu i spomenike.

Hear:

- Iskustva drugih turista na internetu (specifičan sajt X).
- Savete od lokalaca o mestima koja treba posetiti i kulturnim iskustvima koje treba isprobati.
- Priče i anegdote od lokalaca o njihovom kulturnom nasleđu i tradicijama.

Speak & Do:

- Posećuje muzeje, izložbe i istorijske lokacije.
- Prisustvuje kulturnim događajima i festivalima.
- Razgovara sa lokalnim stanovništvom kako bi saznao o njihovoj kulturi.
- Probava lokalnu kuhinju i tradicionalna jela.

Pain:

- Razočaranje zbog prenatrpanih turističkih atrakcija.
- Teškoće u pronalaženju autentičnih kulturnih iskustava usred komercijalizovanih turističkih područja.
- Jezičke barijere pri traženju dubljih kulturnih uvida.
- Nedostatak lokalnih vodiča za istraživanje skrivenih kulturnih dragulja.

Gain:

- Duboko razumevanje lokalnih kultura i tradicija.
- Pronalazak retke umetnosti i istorijskih priča.
- Značajni kontakti (zbližavanje) sa lokalnim stanovništvom.

