Prve dve nedelje drugog sprinta su posvećene razvoju složenih funkcionalnosti. Ovo podrazumeva:

1. Dekompoziciju složenih korisničkih priča na sitnije priče.
2. Planiranje posla na skali od dve nedelje.
3. Dizajniranje i implementacija agregata od više objekata.
4. Jedinično testiranje agregata i integraciono testiranje cele funkcionalnosti.

# 1. Dekompozicija složenih korisničkih priča i planiranje posla
U organizacijama koje prate Scrum radni okvir, _product owner_ rola je zadužena za sprovođenje aktivnosti _backlog grooming_. Ovo je kompozitna aktivnost koja uključuje više koraka, a jedan od tih koraka podrazumeva dekompoziciju velikih ideja za softver u manje korisničke priče. Do razvojnog tima često stižu korisničke priče koje su i dalje krupne i koje vredi usitniti tako da se dobije posao koji se rešava u rasponu od par dana.

Postoji više tehnika za dekompoziciju korisničkih priča, u zavisnosti od prirode same priče. Takođe postoji jedna tehnika koju moramo izbegavati i koja neće proizvesti korisne korisničke priče. Sledeća **[playlista](https://www.youtube.com/watch?v=cGKuogxAmT0&list=PLWTyGVhcibjZvbyNjq2I10K63QreUZIMc)** sabira nekoliko tehnika sa kojim treba da se upoznaš (slobodno slušaj na većoj brzini).

Razlaganje korisničkih priča na sitnije zadatke smanjuje _rizik_ da se veća funkcionalnost neće implementirati i takođe olakšava identifikaciju spregnutosti između priča, čime lakše možemo da pravimo nezavisne (engl. _independent_) korisničke priče.

Većina korisničkih priča koje smo planirali u drugom sprintu podrazumevaju rad od bar dve čovek-nedelje (pod čovek-nedelja mislimo rad od 5-6 sati u sklopu nedelje od strane jednog studenta). Neke zahtevaju pet takvih nedelja.

Da bismo dekomponovali prethodne priče, tim studenata može da prati sledeći algoritam:

1. Klasterovanje priča oko modula koji će se primarno menjati (Stakeholders, Tours, Blog) i podela velikog tima na manje timove za svaki modul. Ako tim nije siguran kom modulu pripada neka kartica, može da konsultuje **[prethodne materijale za izbor modula](https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/back-end.md#a-izbor-modula)**.
2. U okviru svakog podtima, diskusija kako bi se pojedine korisničke priče mogle razložiti primenom tehnika u video materijalima.
3. Formiranje kartica koje uzimaju najviše 2 čovek-nedelje da se reše.
<br><br><br><br>
# 2. Planiranje dvonedeljnog posla
Prost proces planiranja podrazumeva sabiranje zadataka koje treba rešiti, dodeljivanje resursa (ljudi) koji će ih rešiti i organizacija svega na vremenskom toku. Naprednije planiranje podrazumeva i analizu rizika, gde se plan unapređuje tako da se rizici umanje.

Rizik je mogućnost da se nešto loše desi. Kada radimo sa novom tehnologijom, rizik je da se nećemo snaći sa njom za dato vreme. Ako pametno planiramo, takav zadatak ćemo staviti na početak našeg rada kako bismo na vreme videli da li će se rizik ostvariti. Ako se desi (nismo se snašli) možemo da reagujemo i da izdvojimo dodatno vreme za dati posao ili da tražimo pomoć. Ako nespretno planiramo, ostavićemo rizične stvari za poslednji momenat i biti u problemu ako se rizik ostvari.

Plan potreban da se reši zadatak sa malo nepoznanica, od strane jedne osobe i u roku od dva sata je značajno manje _rizičan_ nego plan koji se pravi za projekat na kom radi 20 ljudi 2 godine. Rešavanje zadataka od strane 10 ljudi kroz 2 nedelje ima više rizika.

Sa skupom sitnih korisnička priča, potrebno je da dogovorite ko će šta da radi i u kom redosledu. Dogovor se može rešavati na nivou podtima (stvorenog u koraku 1.1). Pri planiranju, uzmite u obzir sledeće:

1. Postoje tri tipa zavisnosti između kartica koji različito utiču na planiranje:
   1. Dve kartice su _potpuno nezavisne_ kada se rešavaju bez ikakvog uticaja jedna na drugu.<br>
   _Primer_: "ocenjivanje bloga" nema dodira sa "objavljivanjem ture".<br>
   _Uticaj na planiranje_: Dati tip zavisnosti ne utiče na planiranje razvoja.
   2. Dve kartice su _suštinski nezavisne_ kada postoji slaba zavisnost između njih koja se lako može rešiti na početku ili kraju razvoja.<br>
   _Primer_: "simulator pozicije" definiše poziciju turiste koja je potrebna "izvedbi ture". Nakon što je uvedena klasa TouristPosition, moguće je manipulisati podatkom u bazi za potrebe razvoja "izvedbe ture" i pre nego što je kompletan "simulator" gotov).<br>
   _Uticaj na planiranje_: Za dati tip zavisnosti je potrebno iskoordinisati pola sata na početku ili kraju razvoja da se integrišu funkcije.
   3. Dve kartice su _zavisne_ kada je potrebno više sati rada da se integrišu ako se rade u paraleli.<br>
   _Primer_: Ne možemo omogućiti Autoru da "kreira ključne tačke putem mape" ako nismo "integrisali mapu". Možemo doduše da omogućimo autoru da "kreira ključne tačke", gde smo "putem mape" deo izdvojili da se reši nakon što je mapa integrisana.<br>
   _Uticaj na planiranje_: Prvo pokušavamo da dekomponujemo zavisne priče da se izdvoji što manja smislena celina koja je deljena i da se ona prva implementira. U svakom slučaju sekvenciramo posao da se prvo reši zadatak od kog ostali zavise i **ovakve zadatke treba rešiti u prvoj nedelji**.
3. Smisleno je dodeliti ljudima koji su već radili sa nekim modulom zadatak da nastave da rade sa tim modulom. Na većim projektima se timovi formiraju spram modula modularnog monolita (ili servisa kod mikroservisnih arhitektura).
4. Skroz nove vrste zadataka (npr. integracija sa Google Analytics) unose rizik od nepoznatog i ima smisla da se rade pre nego kasnije (ne nužno cela kartica, ali svakako inicijalna integracija).
5. Čak i poznat posao ima inherentan rizik da će nešto iskočiti. Možemo se prehladiti ili se može pojaviti neočekivana situacija u privatnom životu koju moramo da rešavamo. Bolje nam je da odvadimo veću količinu posla u periodu kada je mir. Zbog toga vredi da prva nedelja razvoja podrazumeva da se više posla uradi nego što ostane za drugu. Ako se ostvari rizik, imamo dovoljno vremena u drugoj nedelji da radimo na zadacima. 

Uzimajući sve prethodno u obzir, možemo da raspodelimo posao na nivou tima i ugovorimo u kalendaru ključne rokove da izbegnemo konflikte zbog međuzavisnog rada i da stignemo da potražimo pomoć ako se neki rizik ostvari.
<br><br><br><br>
# 3. Dizajniranje i implementacija agregata
Pre nego što uskočimo u novo gradivo, bitna napomena je da je potrebno srediti korisničku priču i pratiti proces razvoja koji smo videlu u **[prvoj nedelji projekta](https://github.com/psw-ftn/supportive-information/tree/master/s1/w1)**. Ovo podrazumeva:

1. Sređivanje kartice koja definiše zadatak.
2. Izrada koda za serversku (backend) aplikaciju. **Ovaj deo primarno proširujemo**.
3. Izrada koda za klijentsku (frontend) aplikaciju.
4. Otvaranje i dokumentovanje pull requesta.
5. Prepuštanje kolegi da revidira novi kod i odgovaranje na komentare.
6. Zatvaranje pull requesta.

Ključna novina kod implementacije složenijih funkcionalnosti podrazumeva usložnjavanje domenskog sloja uvođenjem šablona za dizajn vođen domenom. Dizajn vođen domenom (engl. _domain-driven design_; DDD) mnogi nazivaju kulminacijom objektno-orijentisanog programiranja. Ovaj pristup je interesantan u projektima koji imaju sofisticiran domen problema, gde je potrebno da ugradimo ozbiljan model tog domena u naš domenski sloj (u našem slučaju u `Core` projekat, `Domain` direktorijum). Naš projekat neće imati preterano sofisticiran domenski model, ali će imati dovoljno složen model da demonstriramo glavne šablone iz DDD sveta.

Da bismo sastavili održivo softversko rešenje i ispunili zahteve za prve dve nedelje S2, neophodno je da se:

1. Upoznamo sa osnovnim taktičkim šablonima iz DDD sveta i primenimo ih na naš zadatak.
2. Implementiramo domenski sloj.
3. Implementiramo perzistenciju potrebnu za podršku navedenih šablona.
4. Ažuriramo ostale slojeve da bismo ispunili zahtev.

### 1. Kreiranje modela taktičkih DDD šablona za kontekst kartice
Za početak je potrebno da se upoznamo sa tri taktička šablona iz DDDa koje nazivamo vrednosni objekat, entitet i agregat. Sa navedenim šablonima ćemo se upoznati kroz niz video materijala koji obrađuju kolekciju klasa prikazanih u nastavku.

![image](https://github.com/psw-ftn/supportive-information/assets/7092212/b71923e8-d30b-408d-9206-3a350b065225)

**[Sledeća playlista](https://www.youtube.com/watch?v=5hxXRIDmH-0&list=PLWTyGVhcibjZ_iwv5wQU_MVTA53k08HB8)** opisuje svojstva ovih šablona. **Napomena**: Druga polovina videa (koji se odnose na agregat) je složenija i naslanja se na prvu polovinu. Preporuka je da se pažljivo isprate materijali i po potrebi napravi pauza na pola da se drugi deo može bolje usvojiti.

Većina kartica u S2 podrazumevaju da se naprave agregati objekata i da se u njih prebaci veći deo poslovne logike. Da bismo ovo postigli, potrebno je da:

1. Analiziramo tekst naše kartice i ostalih kartica koje se tiču istog većeg koncepta u okviru jednog modula. Cilj je da pobrojimo klase domenskog sloja koje su potrebne da podrže tražene funkcionalnosti.
2. Klasifikacija svake klase kao koren agregata, entitet ili vrednosni objekat, gde u opštem slučaju važi:
   1. Koren agregata je entitet koji pored svojih podataka ima asocijaciju ka jednom ili više entitetu i vrednosnom objektu. Ova skupina objekata se koristi zajedno da ispuni slučajeve korišćenja, gde servisi interaguju isključivo sa korenom agregata. Brisanjem korena agregata bismo trebali smisleno da obrišemo i sve povezane objekte. Agregat može da ima jedan objekat, u kom slučaju je to jedan entitet bez dodatnih povezanih objekata.<br>
   _Primer_: Ključna tačka je deo Ture, gde je Tura koren agregata. Problem nastaje kod slučaja korišćenja "prikaži javne ključne tačke". Ovo zahteva da se ključna tačka tretira kao odvojen entitet ili da postoji odvojeni koncept "javne ključne tačke" koji se duplira u Turama koje koriste tu tačku (javna ključna tačka verovatno neće imati tajnu).
   2. Entitet može da bude deo agregata, a da nije njegov koren, kada je jasno podređen drugom entitetu i kada ima svoj životni ciklus.
   3. Vrednosni objekat sadrži kohezivne podatke i logiku koja radi nad njima, ali ne postoji smisleno van agregata.<br>
   _Primer_: Poruka vezana za problem sa turom ne postoji smisleno bez tog problema kom pripada.
3. Izdvajanje dela agregata koji je potreban za implementaciju naše kartice.

_Primer_: Da bismo podržali funkcionalnost vezanu za blog, sprovodimo prethodni algoritam:

1. Blog pored svog sadržaja ima komentare i ocene i možemo da identifikujemo tri klase - `Blog`, `Comment` i `Rating`.
2. Brisanjem bloga ima smisla da obrišemo i sve komentare i ocene vezane za taj blog, što nam je jak indikator da je `Blog` koren agregata. Pošto Blog ima životni ciklus (draft, objavljen, zatvoren, aktivan, poznat) jasno je da je barem entitet. Komentar i ocena nemaju očigledan životni ciklus (npr. nemaju stanje koje bi bio jasan indikator da nekakav životni ciklus postoji). Iako nisu nužno immutable (npr. ima smisla da se edituje komentar) i dalje ih možemo tretirati kao vrednosne objekte. Spram navedenog možemo identifikovati agregat `Blog` koji sadrži dve liste vrednosnih objekata.
3. Funkcionalnosti vezane za davanje glasa i manipulaciju komentara idu kroz `Blog` klasu. Možemo zamisliti `AddRating` metodu koja proverava da li lista `Ratings` sadrži ocenu od datog korisnika. Ako sadrži, zamenjuje je. Ako ne sadrži, dodaje je. Spram ukupne ocene, ista metoda proverava da li treba izmeniti status `Bloga`. Sličnu funkcionalnost vidimo za sve ostale manipulacije Bloga i njegovih objekata, gde bi servis u tom slučaju samo: 1) Učitao `Blog` sa prosleđenim IDem, 2) Pozvao odgovarajuću metodu tog objekta i 3) Vratio rezultat.
4. Interesantno je razmotriti kako ćemo uz blog i komentare prikazati ime (ili korisničko ime) od autora bloga/komentara. Ovo je podatak koji se nalazi u `Stakeholders` modulu i koji ne možemo da referenciramo direktno. Kod modularnog monolita ili mikroservisa imamo tri strategije za rešavanje ovog problema:
   1. Formiranje odvojenog HTTP zahteva kada dobavimo blog sa komentarima da se za sve personId (koji ćemo svakako čuvati u blogu/komentaru) dobavi ime.
   2. Čuvanje redundatnih podataka u vidu imena autora u `Blog` i `Comment` klasama. Dakle, prilikom čuvanja bloga bismo uz tekst bloga poslali i ime osobe koja je napravila blog.
   3. Pozivanje internog APIa `Stakeholders` servisa prilikom dobavljanja bloga u `Blog` servisu. Ovo bi podrazumevalo da:
      1. Definišemo interfejs u `Stakeholders.API/Internal` koji će za date ID-eve vratiti imena ljudi. Potrebno je definisati servis u `Stakeholders.Core` koji implementira taj interfejs i srediti dependency injection. Primer takvog servisa u Tutor projektu je [ovde](https://github.com/Clean-CaDET/tutor/blob/master/src/Modules/Stakeholders/Tutor.Stakeholders.API/Internal/IInternalInstructorService.cs).
      2. U `Blog.Core` ubacimo referencu na projekat `Stakeholders.API`.
      3. U odgovarajućem servisu `Blog.Core` navodimo u konstruktoru interfejs iz `Stakeholders.API/Internal`. U okviru funkcije za dobavljanje bloga pozivamo funkciju internog servisa i spajamo konačan rezultat u odgovarajući DTO (`Blog.API` će morati da definiše svoj DTO za imena ili da u okviru `BlogDto` i `CommentDto` uvede `string` polja za, na primer, ime i prezime). Primer ovakve funkcionalnosti u Tutor projektu je [ovde](https://github.com/Clean-CaDET/tutor/blob/master/src/Modules/Courses/Tutor.Courses.Core/UseCases/Management/GroupMembershipService.cs#L32).
      4. Da bi navedena funkcionalnost mogla da se testira, potrebno je proširiti `BlogTestsFactory.cs` u `Blog.Tests` tako da se doda postavka testne baze za stakeholdere. Na sledećem [linku](https://github.com/Clean-CaDET/tutor/blob/master/src/Modules/Courses/Tutor.Courses.Tests/CoursesTestFactory.cs#L22-L24) se nalazi primer iz Tutora, koji ističe kako `Courses` modul to konfiguriše za svoj `Stakeholders` modul.

### 2. Implementacija domenskog sloja
Sa povećanjem broja klasa u našim projektima, vreme je da razmišljamo o segmentaciji svakog sloja u smislene direktorijume. Za domenski sloj (`Core/Domain`) ima smisla da definišemo 1 direktorijum za svaki agregat ili 1 paket za svaki agregat koji podrazumeva više od jedne klase (dok bi jedno-klasni agregati ostali u `Core/Domain`). Naziv direktorijuma je isti kao naziv korena agregata, samo što je u množini.

Dalje, definišemo klase koje su nam potrebne za rešavanje kartice. Entiteti treba da naslede `Entity` klasu, dok će vrednosni objekti naslediti klasu `ValueObject` i neće imati ID polje. Kada budemo pravili prvi vrednosni objekat, potrebno je da definišemo `ValueObject` klasu koju ćemo smestiti u `BuildingBlocks/Explorer.BuildingBlocks.Core/Domain` (pored `Entity` klase). Primer ove klase i načina njenog nasleđivanja vidimo u **[sledećem članku](https://enterprisecraftsmanship.com/posts/value-object-better-implementation/)**. Uvođenje ove osnovne klase je nešto što treba uraditi samo jednom na početku razvoja, od strane najrevnosnijeg člana tima.

Poslednji korak podrazumeva smeštanje poslovne logike koju agregat treba da podrži u sam agregat. Ovo podrazumeva da se definišu odgovarajuće metode u objektima koje čine agregat. Metode koje nudi koren agregata će servisi kasnije pozivati tako da jedina pamet koju sadrže bude pamet koordinacije više klasa. Ako koren agregata treba da referencira drugi koren agregata, to radi putem IDa.

### 3. Implementacija perzistencije
Kada implementiramo agregate _by the book_, želeli bismo da perzistenciju agregata implementiramo tako da se agregat smešta u i čita iz skladišta u celosti. Ovo podrazumeva dve stvari:

1. U `Domain` direktorijumu ćemo uz koren agregata definisati interfejs repozitorijuma koji je fokusiran na koren agregata. Implementaciju tog repozitorijuma smeštamo u `Infrastructure` projekat.
2. Funkcije za učitavanje agregata koriste `Include` metodu da uključe sve povezane entitete. Prilikom brisanja korena treba kaskadno obrisati i povezane entitete. Dokumentacija za datu metodu je istaknuta [ovde](https://learn.microsoft.com/en-us/ef/ef6/querying/related-data).
3. Pošto vrednosni objekti nemaju ID, njih ćemo skladištiti kao JSON kolone. Da bismo ovo postigli, potrebno je da:
   1. U odgovarajućem `DbContext` nasledniku i u okviru `OnModelCreating` metode definišemo liniju koda `modelBuilder.Entity<MY_ROOT>().Property(item => item.VALUE_OBJECTS).HasColumnType("jsonb");`<br>
   _Primer_: Na **[sledećem linku](https://github.com/Clean-CaDET/tutor/blob/f0f3e136ff23fe4daa6ba9641c6b2a0f9cff0e17/src/Modules/KnowledgeComponents/Tutor.KnowledgeComponents.Infrastructure/Database/KnowledgeComponentsContext.cs#L78-L79)** se vidi primer konfiguracije.
   2. U klasi koja nasleđuje `ValueObject` ubacujemo konstruktor koji prihvata sve parametre i ima `[JsonConstructor]` anotaciju.<br>
   _Primer_: Na **[sledećem linku](https://github.com/Clean-CaDET/tutor/blob/f0f3e136ff23fe4daa6ba9641c6b2a0f9cff0e17/src/Modules/KnowledgeComponents/Tutor.KnowledgeComponents.Core/Domain/Knowledge/AssessmentItems/Hint.cs#L11)** se vidi primer konstruktora.
   3. Po potrebi se modifikuje mapiranje domenskih objekata na DTO i obratno, tako da se eksplicitno poziva konstruktor vrednosnog objekta.<br>
   _Primer_: Na **[sledećem linku](https://github.com/Clean-CaDET/tutor/blob/f0f3e136ff23fe4daa6ba9641c6b2a0f9cff0e17/src/Modules/KnowledgeComponents/Tutor.KnowledgeComponents.Core/Mappers/AssessmentItemsProfile.cs#L17-L18)** se vidi primer konfiguracije.

Pošto agregati predstavljaju skup povezanih objekata koji se zajedno učitavaju, skladište i uništavaju zajedno, često se koriste druge vrste skladišta koje nisu SQL baze podataka. Tipičan primer baze pogodne za skladištenje agregata su NoSQL baze. Da bismo izbegli uvođenje nove tehnologije, koristimo funkcionalnosti koje PostgreSQL pruža da skladišti JSON dokumente.

_Primer_: Za `Blog` ćemo:

1. Definisati interfejs repozitorijuma u domenskom sloju i implementaciju repozitorijuma u `Infrastructure` projektu.
2. Pošto `Blog` nema povezane entitete u primeru koji smo iznad obrađivali, implementacija repozitorijuma je prosta (i možemo se čak osloniti na `CrudRepository` ako nemamo dodatne metode).
3. `Blog` ima 2 vrednosna objekta i za njih ćemo definisati mapiranje u `BlogContext` klasi na `jsonb`. Takođe dodajemo u svaku klasu konstruktor sa ispravnom anotacijom. Dodatno sređujemo mapiranje u `BlogProfile` klasi (`Core/Mappers`).

### 4. Implementacija ostalih slojeva
Da bismo podržali kompletne funkcionalnosti, neophodno je da pored domenskih slojeva i repozitorijuma imamo odgovarajuće servise i kontrolere.

Pošto nam raste broj kontrolerskih i servisnih klasa, postavlja se pitanje kako ima smisla da ih grupišemo u direktorijume. Odgovor koji nam se uklapa u arhitekturu jeste da servise grupišemo po grupama slučajeva korišćenja, dok ćemo kontrolere prvo grupisati po ulozi (kao što je sada), a onda dodatno u okviru svake uloge po grupama slučajeva korišćenja. Pitanje je šta su "grupe slučajeva korišćenja"? U našem projektu za sada imamo sledeće grupe slučajeva korišćenja:

- `Shopping` - sve funkcionalnosti koje podržavaju turistu u kupovini.
- `Authoring` - sve funkcionalnosti koje podržavaju autora u konstrukciji ture.
- `Execution` - sve funkcionalnosti koje podržavaju turistu prilikom vođenja ture.
- `Blog` - sve funkcionalnosti vezane za podsistem za blog (pošto je ovo već samostalan modul, nema smisla dodatno segmentirati servise tog modula).
- `Administration` - sve funkcionalnosti koje podržavaju administratora da održava sistem.
- `Identity` - sve funkcionalnosti za održavanje svog digitalnog identiteta od strane korisnika.

Prve tri gupe slučajeva korišćenja su podržana od strane `Tours` modula. Četvrta je iz istoimenog modula, dok su peta i šesta primarno vezani za `Stakeholders` modul.

Što se tiče samih servisa i kontrolera, ovde nema previše izmena u odnosu na prošli put. Pošto sad radimo sa agregatima, teško ćemo koristiti prosti `CrudService` da podržimo naprednije funkcionalnosti. Pošto je većina pameti u samom agregatu, servis treba da 1) Učita 1 ili više agregata koji su potrebni da se ispuni slučaj korišćenja, 2) Traži od učitanih agregata da urade svoj posao i koordiniše njihovu interakciju kada treba, 3) Formira rezultat i sačuva izmene agregata ako ih je bilo.

Sami kontroleri trebaju da definišu odgovarajuće endpointe, no ovo se ne razlikuje u odnosu na ono što smo imali ranije.
<br><br><br><br>
# 4. Testiranje agregata
TODO
TODO: Napomena za testnu skriptu.
