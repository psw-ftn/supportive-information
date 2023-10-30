Prve dve nedelje drugog sprinta su posvećene razvoju složenih funkcionalnosti. Ovo podrazumeva:

1. Dekompoziciju složenih korisničkih priča na sitnije priče.
2. Planiranje posla na skali od dve nedelje.
3. Dizajniranje i implementacija agregata od više objekata.
4. Jedinično testiranje agregata i integraciono testiranje cele funkcionalnosti.

# 1. Dekompozicija složenih korisničkih priča
U organizacijama koje prate Scrum radni okvir, _product owner_ rola je zadužena za sprovođenje aktivnosti _backlog grooming_. Ovo je kompozitna aktivnost koja uključuje više koraka, a jedan od tih koraka podrazumeva dekompoziciju velikih ideja za softver u manje korisničke priče. Do razvojnog tima često stižu korisničke priče koje su i dalje krupne i koje vredi usitniti tako da se dobije posao koji se rešava u rasponu od par dana.

Postoji više tehnika za dekompoziciju korisničkih priča, u zavisnosti od prirode same priče. Takođe postoji jedna tehnika koju moramo izbegavati i koja neće proizvesti korisne korisničke priče. Sledeća **[playlista](https://www.youtube.com/watch?v=cGKuogxAmT0&list=PLWTyGVhcibjZvbyNjq2I10K63QreUZIMc)** sabira nekoliko tehnika sa kojim treba da se upoznaš (slobodno slušaj na većoj brzini).

Razlaganje korisničkih priča na sitnije zadatke smanjuje _rizik_ da se veća funkcionalnost neće implementirati i takođe olakšava identifikaciju spregnutosti između priča, čime lakše možemo da pravimo nezavisne (engl. _independent_) korisničke priče.

Većina korisničkih priča koje smo planirali u drugom sprintu podrazumevaju rad od bar dve čovek-nedelje (pod čovek-nedelja mislimo rad od 5-6 sati u sklopu nedelje od strane jednog studenta). Neke zahtevaju pet takvih nedelja.

Da bismo dekomponovali prethodne priče, tim studenata može da prati sledeći algoritam:

1. Klasterovanje priča oko modula koji će se primarno menjati (Stakeholders, Tours, Blog) i podela velikog tima na manje timove za svaki modul. Ako tim nije siguran kom modulu pripada neka kartica, može da konsultuje **[prethodne materijale za izbor modula](https://github.com/psw-ftn/supportive-information/blob/master/s1/w1/back-end.md#a-izbor-modula)**.
2. U okviru svakog podtima, diskusija kako bi se pojedine korisničke priče mogle razložiti primenom tehnika u video materijalima.
3. Formiranje kartica koje uzimaju najviše 2 čovek-nedelje da se reše. Možete ubaciti _powerup_ na vašu trelo tablu za ove [poene](https://trello.com/power-ups/638372c5e00ec1016bb45460/story-points-for-trello) (zahteva refresh stranice kad se ubaci).
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
   _Primer_: Ključna tačka je deo Ture, gde je Tura koren agregata. Problem nastaje kod slučaja korišćenja "prikaži javne ključne tačke". Ovo zahteva da se ključna tačka tretira kao odvojen entitet ili da postoji odvojeni koncept "javne ključne tačke" koji se duplira u Turama koje koriste tu tačku (javna ključna tačka verovatno neće imati tajnu). Ako odaberemo prvu opciju (odvojen entitet), onda bi Tura čuvala listu IDeva ključnih tačaka u okviru svog agregata, a po potrebi bi se spram te liste učitavala lista ključnih tačaka. Zbog ove komplikacije bi druga opcija predstavljala elegantnije rešenje.
   2. Entitet može da bude deo agregata, a da nije njegov koren, kada je jasno podređen drugom entitetu i kada ima svoj životni ciklus.
   3. Vrednosni objekat sadrži kohezivne podatke i logiku koja radi nad njima, ali ne postoji smisleno van agregata.<br>
   _Primer_: Poruka vezana za problem sa turom ne postoji smisleno bez tog problema kom pripada.
3. Dizajniranje atributa i metoda agregata koji je potreban za implementaciju naše kartice.

_Primer_: Da bismo podržali funkcionalnost vezanu za blog, sprovodimo prethodni algoritam:

1. Blog pored svog sadržaja ima komentare i ocene i možemo da identifikujemo tri klase - `Blog`, `Comment` i `Rating`.
2. Pošto Blog ima životni ciklus (draft, objavljen, zatvoren, aktivan, poznat) jasno je da je barem entitet. Brisanjem bloga ima smisla da obrišemo i sve komentare i ocene vezane za taj blog, što nam je jak indikator da je `Blog` koren agregata. Komentar i ocena nemaju očigledan životni ciklus (npr. nemaju stanje koje bi bio jasan indikator da nekakav životni ciklus postoji). Iako nisu nužno immutable (npr. ima smisla da se edituje komentar) i dalje ih možemo tretirati kao vrednosne objekte. Spram navedenog možemo identifikovati agregat `Blog` koji sadrži dve liste vrednosnih objekata.
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
Automatski testovi koje smo do sada pisali su testirali relativno jednostavnu logiku, gde je kontroler pozivao servis koji je vršio prostu koordinaciju da ažurira ili dobavi neki entitet. Uvođenjem agregata objekata i formiranjem nešto složenije logike u domenskom sloju imamo potrebu da napišemo više testova kako bismo proverili da se tražene funkcionalnosti ponašaju ispravno.

Sada ćemo imati potrebu da testiramo istu funkcionalnost više puta, gde menjamo ulazne podatke i testne podatke za svako pokretanje. Na primer, ako imamo endpoint čiji zadatak je da objavi turu, želeli bismo da sa automatskim testovima pokrijemo:

- Poziv endpointa tako da se tura uspešno objavi.
- Poziv endpointa gde tura nije u validnom stanju za objavu, gde bismo hteli po jedan test za svako validaciono pravilo (npr. za status, osnovne informacije, broj ključnih tačaka i vreme).
- Poziv endpointa od strane autora koji nije vlasnik ture.

Iz navedenog vidimo da će nam trebati 5-6 testova koji će imati sličan kod. Primer dva takva testa vidimo u nastavku:
```csharp
[Fact]
public void Publish_succeeds()
{
    // Arrange - Input data
    var authorId = "-1";
    var tourId = -5;
    var expectedResponseCode = 200;
    var expectedStatus = TourStatus.Published;
    // Arrange - Controller and dbContext
    using var scope = Factory.Services.CreateScope();
    var controller = CreateController(scope, authorId);
    var dbContext = scope.ServiceProvider.GetRequiredService<ToursContext>();

    // Act
    var result = (ObjectResult)controller.Publish(tourId).Result;

    // Assert - Response
    result.ShouldNotBeNull();
    result.StatusCode.ShouldBe(expectedResponseCode);
    // Assert - Database
    var storedEntity = dbContext.Tours.FirstOrDefault(t => t.Id == tourId);
    storedEntity.ShouldNotBeNull();
    storedEntity.Status.ShouldBe(expectedStatus);
}

[Fact]
public void Publish_fails_invalid_checkpoints()
{
    // Arrange - Input data
    var authorId = "-1";
    var tourId = -4;
    var expectedResponseCode = 422;
    var expectedStatus = TourStatus.Draft;
    // Arrange - Controller and dbContext
    using var scope = Factory.Services.CreateScope();
    var controller = CreateController(scope, authorId);
    var dbContext = scope.ServiceProvider.GetRequiredService<ToursContext>();
    
    // Act
    var result = (ObjectResult)controller.Publish(tourId).Result;

    // Assert - Response
    result.ShouldNotBeNull();
    result.StatusCode.ShouldBe(expectedResponseCode);

    // Assert - Database
    var storedEntity = dbContext.Tours.FirstOrDefault(t => t.Id == tourId);
    storedEntity.ShouldNotBeNull();
    storedEntity.Status.ShouldBe(expectedStatus);
}

private static EquipmentController CreateController(IServiceScope scope, string personId)
{
    return new EquipmentController(scope.ServiceProvider.GetRequiredService<IEquipmentService>())
    {
        ControllerContext = BuildContext(personId)
    };
}
```
Prethodni testovi prave pretpostavku da u testnim skriptama postoje Ture sa ID-em -4 i -5 čije stanje odgovara situaciji koja se testira (-5 je tura sa svim podacima, a -4 nema 2 ključne tačke, što je zahtev za validaciono pravilo).

Većina testnog koda za dva primera i sve ostale testove je identična. Jedina razlika je na vrhu testa, gde se definišu parametri testa. Kod automatskih testova, slično kao kod funkcija, možemo da uvedemo parametre za ove potrebe uz pomoć `[Theory]` anotacije. Prethodan primer se transformiše na sledeći način:

```csharp
[Theory]
[InlineData("-1", -5, 200, TourStatus.Published)]
[InlineData("-1", -4, 422, TourStatus.Draft)]
public void Publishes(string authorId, long tourId, int expectedResponseCode, TourStatus expectedStatus)
{
    // Arrange
    using var scope = Factory.Services.CreateScope();
    var controller = CreateController(scope, authorId);
    var dbContext = scope.ServiceProvider.GetRequiredService<ToursContext>();
    
    // Act
    var result = (ObjectResult)controller.Publish(tourId).Result;

    // Assert - Response
    result.ShouldNotBeNull();
    result.StatusCode.ShouldBe(expectedResponseCode);

    // Assert - Database
    var storedEntity = dbContext.Tours.FirstOrDefault(t => t.Id == tourId);
    storedEntity.ShouldNotBeNull();
    storedEntity.Status.ShouldBe(expectedStatus);
}
```
Kada su parametri koje prosleđujemo primitive, možemo koristiti `InlineData` anotaciju, kao što primer ilustruje. Ovaj kod bismo mogli proširiti sa 4-5 dodatne `InlineData` linije koda da pokrijemo sve prethodno navedene testne slučajeve. Naravno, morali bismo da dopunimo testne skripte da se svaka tura ubaci.

U situacijama kada želimo da složenije objekte definišemo putem parametra, potrebno je da koristimo `[MemberData]` anotaciju. **[Sledeći primer](https://github.com/Clean-CaDET/tutor/blob/f0f3e136ff23fe4daa6ba9641c6b2a0f9cff0e17/src/Modules/KnowledgeComponents/Tutor.KnowledgeComponents.Tests/Integration/Learning/Assessment/SubmissionMcqTests.cs#L15-L76)** ilustruje kako to izgleda. Sintaksa deluje strašno, ali je u pitanju jednostavan šablon. Ključna je `McqSubmissions` funkcija koja vraća `IEnumerable<object[]>`. Po jedan test će se pokrenuti za svaki `object[]` koji je definisan, gde se redom uzimaju elementi ovog niza i postavljaju kao vrednosti parametra testa.

### Code coverage
Bitna metrika kod automatskog testiranja predstavlja % pokrivenosti koda od strane testova (engl. *code coverage*). Kada imamo funkciju koja sadrži 10 linija koda, od kojih je 4 u IF bloku, a 4 u ELSE bloku, test koji aktivira samo prvi uslovni blok će pokriti oko 50% koda funkcije. Kod koji je domenski značajan i algoritamski složen je bitno što temeljnije istestirati, što obično podrazumeva visok *code coverage*.

Kada koristimo *ReSharper* plugin za *Visual Studio*, možemo da aktiviramo funkcionalnost za računanje ove metrike putem sledeće komande:

![image](https://github.com/psw-ftn/supportive-information/assets/7092212/e780945f-8d17-44fc-bfbb-4440679ab6ff)

Panel koji ćemo dobiti ima sledeći izgled:

![image](https://github.com/psw-ftn/supportive-information/assets/7092212/cf7d15f6-b5b1-43b5-b99a-a21bc6355e73)

Interesantno nam je da `Domain` namespace svakog modula ima što veći stepen pokrivenosti (>85% je dobra mera), a slično važi i za `UseCases`. Kada smo ovo pokrili, dobra je šansa da će u ostatku aplikacije većina koda biti pokrivena.

### Alternative za testiranje agregata
Svi testovi koje smo do sada pisali su **integracioni testovi**. Integracioni testovi testiraju složenije funkcionalnosti koje uključuju neku poslovnu logiku, ali i koordinaciju većeg broja objekata i potencijalno većeg broja aplikacija. U našem slučaju, integracioni testovi pored funkcija naše .NET aplikacije uključuju i interakciju sa (testnom) bazom.

Za razliku od integracionih testova, jedinični testovi gađaju manji skup objekata koji je isključivo vezan za našu aplikaciju i najčešće pripada domenskom sloju. Sa jediničnim testovima se fokusiramo da istestiramo sve varijante ponašanja domenskog sloja bez da se opterećujemo sa bazom podataka i drugim brigama koje dolaze kada testiramo kompletnu funkcionalnost aplikacije, od kontrolera na dalje. Ovakvi testovi se brže pokreću (ne treba nam baza) i lakše održavaju (nemamo SQL skripte). Mana je što su ovakvi testovi slabo otporni na refaktorisanje koda koji se testira. Ovo znači da će izmene agregata koji se testira često zahtevati i izmenu jediničnog testa koji testira dati agregat.

Testni kod jediničnog testa je dosta jednostavniji. Za prethodni primer, testovi bi imali sledeći oblik:

```csharp
[Theory]
[InlineData(-5, true, TourStatus.Published)]
[InlineData(-4, false, TourStatus.Draft)]
public void Publishes(long tourId, bool expectedSuccess, TourStatus expectedStatus)
{
    // Arrange
    var tour = GetTestTour(tourId);
    
    // Act
    var result = tour.Publish();

    // Assert
    result.IsSuccess.ShouldBe(expectedSuccess);
    result.Value.Status.ShouldBe(expectedStatus);
}

private static Tour GetTestTour(long tourId)
{
    // Definiši listu tura za potrebe testiranja
    // Vrati turu čiji ID je jednak tourId
}
```

Sa prethodnim testovima se fokusiramo na validnost poslovnih pravila definisanih u okviru `Tour` klase. Sa ovim pristupom ne možemo da testiramo da li autor ima pravo da objavi turu (da li je vlasnik ture) pošto je ovo logika koju bismo definisali u servisu (i pokrili bismo je integracionim testom).

### Bitne napomene

- Pošto ćemo vrednosne objekte serijalizovati u json kolone, potrebno je da obratimo pažnju na specifično ponašanje koje pronalazimo u testnim SQL skriptama. Ako želimo da u testnu bazu ubacimo JSON objekat i koristimo za to vitičaste zagrade ("{" i "}"), neophodno je da na svakom mestu gde ih koristimo u testnoj skripti uduplamo zagrade (da bude "{{" i "}}").
- Ponavljamo **napomenu** od prošle nedelje: Ako `TestData` skripte sadrže grešku, testovi će se pokrenuti sa testnom bazom koja nije u predviđenom stanju. Posledično će neki testovi pući. Pored log zapisa na konzolu, možeš da postaviš breakpoint u `BuildingBlocks.Tests` projektu na [sledećoj liniji koda](https://github.com/psw-ftn/tourism-be/blob/27211b3bc9e92ed280d684d1f59562eee628ac98/src/BuildingBlocks/Explorer.BuildingBlocks.Tests/BaseTestFactory.cs#L48). Zatim pokreni testove u debug režimu rada i proveri da li se ovaj problem dešava.
