Serverski deo aplikacije je izgrađen koristeći:

- `ASP.NET` radni okvir za izgradnju Web aplikacije,
- `Entity Framework` biblioteku za objektno-relaciono mapiranje (pretvaranje objekata u redove SQL tabela i obratno),
- `AutoMapper` biblioteke za pretvaranje DTO instanci u domenske objekte i obratno,
- `xUnit` radni okvir za pisanje automatskih testova.
- `PostgreSQL` bazu podataka sa `pgAdmin` aplikacijom za upravljanje bazom podataka.

Postepeno ćemo se upoznavati sa svim tehnologijama i kroz kurs ćemo sve pametnije stvari moći da radimo sa njima. Ova stranica sadrži smernice za izradu jednostavne funkcionalnosti u serverskom delu aplikacije, gde ćemo videti:
<ol start="0">
  <li>Kako je organizovan projekat i kako se pokreće.</li>
  <li>Kako da dodamo novu domensku klasu koja nam treba za ispunjenje zahteva.</li>
  <li>Kako da definišemo servis koji radi sa tom klasom i vraća DTO.</li>
  <li>Kako da definišemo kontroler koji se aktivira putem HTTP zahteva.</li>
  <li>Kako da sačuvamo instance domenske klase u bazi podataka.</li>
  <li>Kako da ažuriramo dependency injection.</li>
  <li>Kako da napišemo automatski test koji proverava da sve radi.</li>
</ol>

Nulti korak ćeš raditi samo jednom u potpunosti, dok ćeš korake 1 do 6 raditi svaki put kad razvijaš skroz novu funkcionalnost. Redosled koraka 1 do 6 ne mora da prati naveden, no dobro je da prvi put ispratiš dati redosled.
<br/><br/><br/><br/>
## 0. Organizacija i pokretanje projekta
Prvi put kad sedneš da radiš na projektu ćeš morati da **kloniraš repozitorijum** svog tima na svoju mašinu. Ovde će ti pomoći `git clone` komanda uz URL repozitorijuma tima.

Preporuka je da otvoriš Solution u svom razvojnom okruženju (naša preporuka je Visual Studio) i da ga istražiš pre nego što nastaviš da čitaš.

### a. Organizacija Solutiona
Solution se sastoji od više projekata i paketa. Prvа celina sadrži gradivne elemente celokupnog projekta koji ćeš ostatak koda koristiti:
```
BuildingBlocks                              - Sadrži common klase, odnosno klase koje su korisne svim modulima od modularnog monolita.
  -> Explorer.BuildingBlocks.Core           - Klase koje su korisne svim API i Core projektima.
  -> Explorer.BuildingBlocks.Infrastructure - Klase koje su korisne Infrastructure projektima.
  -> Explorer.BuildingBlocks.Tests          - Klase koje su korisne Tests projektima.
```
BuildingBlocks paket će se retko menjati tokom kursa i ne treba da ga diramo u prvom sprintu.

Većina izmena će se dešavati u različitim modulima našeg modularnog monolita:
```
Modules                             - Sadrži sve module (package-by-feature) od modularnog monolita.
  -> Blog                           - Modul koji se bavi funkcionalnostima vezanim za Blog.
    -> Explorer.Blog.API            - API projekat definiše interfejse modula koje će implementirati servisne klase u Core projektu. Uz to definiše i  DTO klase modula.
    -> Explorer.Blog.Core           - Core projekat sadrži domenski i servisni sloj. Ovo je jedino mesto gde ćemo imati poslovnu logiku i većinu želimo da postavimo upravo u domenski sloj.
    -> Explorer.Blog.Infrastructure - Infrastructure projekat sadrži repozitorijume i ostale infrastrukturne servise koje ćemo vremenom dodavati u projekat.
    -> Explorer.Blog.Tests          - Tests projekat sadrži automatske testove koji proveravaju da li je naš kod ispravan.
  -> Stakeholders                   - Modul koji se bavi funkcionalnostima vezanim za registraciju korisničkih profila i komunikacijom između njih
    -> ...
  -> Tours                          - Modul koji se bavi funkcionalnostima vezanim za prodaju i izvršavanje tura
    -> ...
```
U startu ćemo imati 3 modula, a kako projekat bude rastao ćemo dodati još. Na kraju vidimo još dva projekta:
```
Explorer.API                        - Definiše kontrolerske klase koje se aktiviraju uz pomoć HTTP zahteva koji nam stižu sa Angular aplikacije.
Explorer.Architecture.Tests         - Definiše automatske testove koji proveravaju da li je naša arhitektura i dalje ispravna.
```
`Explorer.API` projekat ćemo proširivati kada god želimo da ponudimo novu funkciju klijentskoj aplikaciji. `Explorer.Architecture.Tests` projekat nećemo nikad dirati, već ćemo koristiti ove testove da ispratimo da li je arhitektura ispoštovana.

### b. Podešavanje baze podataka za regularnu upotrebu
Da bi aplikacija mogla da se koristi, potrebno je podesiti bazu podataka tako što ćeš:

1. Osposobiti konekciju ka bazi.
2. Definisati potrebne šeme.
3. Pokrenuti migracije koje automatski kreiraju tabele.

Navedeni koraci su sabrani u **video materijalu** radi lakšeg snalaženja. TODO

#### 1. Osposobljavanje konekcije ka bazi
U okviru `Explorer.BuildingBlocks.Infrastructure` projekta se nalazi klasa `DbConnectionStringBuilder`. Ovde je definisan kod putem kog se aplikacija kači na bazu. Izdvajamo delove koda na koje treba obratiti pažnju:
```
var port = Environment.GetEnvironmentVariable("DATABASE_PORT") ?? "5432";
var database = Environment.GetEnvironmentVariable("DATABASE_SCHEMA") ?? "explorer-v1";
var user = Environment.GetEnvironmentVariable("DATABASE_USERNAME") ?? "postgres";
var password = Environment.GetEnvironmentVariable("DATABASE_PASSWORD") ?? "super";
```
Navedeni kod ističe na kom portu bi trebala baza podataka da bude podignuta, kako treba da se nazove kreirana baza i šta su kredencijali korisnika koji ima pristup datoj bazi.
Kako se podešava port baze i kredencijali korisnika možeš da saznaš uz Gugl ili GPT upit. Kreiranje nove baze sa `explorer-v1` nazivom ćeš rešiti kroz `pgAdmin` aplikaciju.

**Kako biste izbegli konflikte, naša preporuka je da svaki član tima postavi istaknute podatke lokalno kod sebe umesto da menja kod u `Infrastructure` projektu.**

#### 2. Definisanje šema
Kada si napravio bazu sa traženim podacima, potrebno je da definišeš po jednu šemu u okviru `explorer-v1` baze za svaki modul, što možeš sa sledećim komandama:
```
CREATE SCHEMA "stakeholders";
CREATE SCHEMA "tours";
CREATE SCHEMA "blog";
```

#### 3. Pokretanje migracija
Biblioteka koju koristimo da radimo sa bazom, `Entity Framework` nudi mehanizam za automatsko kreiranje tabela u bazi podataka. Da bismo aktivirali ovu funkcionalnost, potrebno je da pokrenemo sledeću komandu u `package manager console` prozoru (u okviru Visual Studia).

```
Add-Migration -Name Init -Context StakeholdersContext -Project Explorer.Stakeholders.Infrastructure -StartupProject Explorer.API
Update-Database -Context StakeholdersContext -Project Explorer.Stakeholders.Infrastructure -StartupProject Explorer.API

Add-Migration -Name Init -Context ToursContext -Project Explorer.Tours.Infrastructure -StartupProject Explorer.API
Update-Database -Context ToursContext -Project Explorer.Tours.Infrastructure -StartupProject Explorer.API

Add-Migration -Name Init -Context BlogContext -Project Explorer.Blog.Infrastructure -StartupProject Explorer.API
Update-Database -Context BlogContext -Project Explorer.Blog.Infrastructure -StartupProject Explorer.API

```
Prethodna komanda će u svakom `Infrastructure` projektu da generiše datoteke za migraciju (Add-Migration komanda) i da napravi potrebne tabele u bazi (Update-Database komanda).

### c. Testiranje pokrenute aplikacije
Kada je baza podataka konfigurisana i migracije izvršene, trebalo bi da možeš da pokreneš serversku aplikaciju i da interaguješ sa njom putem klijentske aplikacije ili putem `Swagger` biblioteke koja će iskočiti kada se serverska aplikacija pokrene.

Sledeći **video** TODO prikazuje kako `Swagger` može da se koristi da testira rad aplikacije. Kroz isti video prolazimo standardan tok podataka - od kontrolera, preko servisa, do baze podataka i nazad.

<br/><br/><br/><br/><br/><br/>
## 1. Kreiranje domenske klase
Kad god pristupimo rešavanju nove korisničke priče, potrebno je da **otvorimo novu granu** koju ćemo izvući iz `development` grane. Ovo radimo putem `git branch feat/IME_FEATURA` komande. Nakon kreiranja grane, možemo da uradimo `git checkout feat/IME_FEATURA` i da krenemo sa razvojem.

Većina zadataka u prvoj nedelji podrazumevaju izradu novog entiteta u domenskom sloju. Za ovaj zadatak je potrebno da:
<ol type="a">
  <li>Odabereš dobar modul u koji smeštamo novu klasu.</li>
  <li>Kreiraš entitet u odgovarajućem `Core` projektu.</li>
</ol>

### a. Izbor modula
U startu počinjemo sa tri modula:

1. Stakeholders - Modul koji se bavi funkcionalnostima vezanim za registraciju korisničkih profila i komunikacijom između njih.
2. Tours - Modul koji se bavi funkcionalnostima vezanim za prodaju i izvršavanje tura.
3. Blog - Modul koji se bavi funkcionalnostima vezanim za blog.

Izazov je odrediti kom modulu pripada novi entitet, spram opisa odgovornosti modula. U takvim situacijama potrebno je da postavimo sledeća dva pitanja kada se pitamo da li entitet **E** treba smestiti u modul **M**:

1. Ako biznis za koji pravim softver odluči da im ne treba modul M, da li brisanje modula M smisleno povlači i uklanjanje podataka vezanih za E (alternativa je da E ipak treba da ostane u sistemu)?
2. Da li operacije koje rade sa E većinski koriste podatke iz M (alternativa je da većinski koriste podatke iz drugog modula)?

Ako je odgovor DA na oba pitanja, E pripada M. Ako je odgovor NE na oba pitanja, E ne pripada M. Problem nastaje kada je odgovor na prvo pitanje DA, a na drugo NE. U tom slučaju treba da vagamo u kojoj meri operacije nad E koriste podatke iz drugih modula i da presečemo gde ima smisla da smestimo date funkcionalnosti.

### b. Kreiranje entiteta.
Da bismo kreirali novi entitet, potrebno je da:

1. U okviru `Core` projekta odgovarajućeg modula otvorimo `Domain` direktorijum i u okviru njega napravimo klasu sa značajnim nazivom.
2. Nova klasa nasleđuje `Entity` klasu iz `BuildingBlocks.Core` projekta.
3. Nova klasa definiše polja koja odgovaraju zahtevu, gde stavljamo sve `set` metode na privatne ili ih zamenjujemo sa `init` (vrednost polja može da se postavi samo pri konstrukciji).
4. Nova klasa ima konstruktor sa parametrima koji odgovaraju svim poljima. Konstruktor treba da validira prosleđene parametre.

**Primer**: Domenska klasa [Equipment.cs](https://github.com/psw-ftn/tourism-be/blob/32e92f2f6f42094ff89aae6a90aaf25cb0780f1d/src/Modules/Tours/Explorer.Tours.Core/Domain/Equipment.cs) iz početnog projekta.

Kako nam složenost projekta bude rasla videćemo da izdelimo `Domain` direktorijum na poddirektorijume.
<br/><br/><br/><br/><br/><br/>
## 2. Kreiranje servisa modula
Da bismo osposobili kompletan servis koji će pružati funkcionalnosti, potrebno je da:

<ol type="a">
  <li>Definišeš interfejs servisa i povezane DTO.</li>
  <li>Definišeš implementacije servisa i DTO-Domain mapiranja.</li>
</ol>

### a. Definisanje interfejsa servisa i DTO klase
Interfejse servisa i DTO klase definišemo u okviru `API` projekta povezanog modula. Ovaj projekat sadrži tri veća direktorijuma:
```
Dtos      - Definiše DTO klase koje dolaze sa klijentske aplikacije.
Internal  - Definiše interne interfejse servisa modula koje će koristiti drugi moduli (ovo nam ne treba u prvoj nedelji).
Public    - Definiše javne interfejse servisa koje će pozivati kontroleri.
```
Potrebno je da:

1. Definišeš odgovarajuću DTO klasu koja će se mapirati na domensku klasu iz prethodnog koraka. **DTO klasa, za razliku od domenske klase, treba da ima javne get i set metode.**
2. Definišeš interfejs datoteku za tvoj servis koja će izlistati sve metode koje treba da podržiš za svoju korisničku priču i **ništa van toga**. Metode prihvataju i vraćaju DTO klase, a ne domenske klase.

### b. Definisanje implementacije servisa i mapiranje
Implementacije servisa se smeštaju u `Core` projekat povezanog modula. Ovaj projekat sadrži tri veća direktorijuma:
```
Domain   - Definiše klase iz domenskog sloja.
Mappers  - Konfiguriše "AutoMapper" biblioteku da automatski mapira DTO klase na domenske i obratno.
UseCases - Definiše koordinatorske klase iz servisnog sloja.
```
Potrebno je da:

1. U okviru konstruktora `Mappers/_MODULE_Profile` klase konfigurišeš mapiranje DTO klase na domenski objekat. U prostom slučaju ćeš za ovo iskoristiti sledeći kod: `CreateMap<_ENTITY_Dto, _ENTITY_>().ReverseMap();`. Za naprednija mapiranja istraži **<a href="https://docs.automapper.org/en/stable/Projection.html" target="_blank">dokumentaciju</a>**.
2. Definišeš servisnu klasu koja implementira povezani interfejs iz `API` projekta. Klasu smeštaš u `UseCases`.
3. Implementiraš servisnu klasu (detalji ispod).

#### Implementacija servisne klase
U okviru `BuildingBlocks.Core` projekta smo definisali 2 osnovne servisne klase koje tvoje servisne klase mogu da naslede. Bitno je da razumeš pod kojim okolnostima ćeš koristiti koju klasu:

1. `CrudService` implementira `Create`, `Read` (one i many), `Update` i `Delete` funkcije i koristan je da brzo osposobimo prostu CRUD funkcionalnost. Pošto nam je ovo zadatak za prvu nedelju, sve što treba da uradimo jeste da nasledimo ovu klasu i definišemo konstruktor koji će kroz *Dependency Injection* dobiti potrebne klase i proslediće ih roditelju. Za primer analiziraj 
2. `BaseService` sadrži pomoćne metode za mapiranje domenskih objekata na DTO i obratno. Ovu klasu nasleđujemo kada naš servis: 1) radi većinski sa jednim entitetom i 2) ima metode koje se većinski ne preklapaju sa `CrudService` (npr. potrebne su samo 2 CRUD operacije i/ili ima više svojih metoda).

**Primer**: Servisna CRUD klasa [EquipmentService.cs](https://github.com/psw-ftn/tourism-be/blob/32e92f2f6f42094ff89aae6a90aaf25cb0780f1d/src/Modules/Tours/Explorer.Tours.Core/UseCases/Administration/EquipmentService.cs) iz početnog projekta.
<br/><br/><br/><br/><br/><br/>
## 3. Kreiranje kontrolera
Kontrolerske klase koriste `ASP.NET` anotacije kako bi radni okvir pozvao njihove metode kada se odgovarajući HTTP zahtev izvrši. Sve kontrolerske klase su definisane u okviru `Explorer.API` projekta, koji je ujedno i jedini projekat koji zavisi od `ASP.NET` tehnologije.

Potrebno je da:
<ol type="a">
  <li>Odrediš gde da postaviš kontrolersku klasu koja će pozivati novi servis. Kontrolerske klase se nalaze unutar `Controllers` direktorijuma, koji je dalje segmentiran spram korisničkih rola. Čitajući tekst korisničke priče (As a... deo) možemo da odredimo u koji direktorijum treba da smestimo novi kontroler.</li>
  <li>Implementiraš kontrolersku klasu (detalji ispod).</li>
</ol>

### b. Implementacija kontrolerske klase
Nakon definisanja kontrolerske klase, potrebno je da implementiraš sledeće:

1. Klasa treba da nasledi `BaseApiController` i da iznad svog naziva sadrži anotacije `[Authorize(Policy = "_ROLE_Policy")]` i `[Route("api/_USE_CASE_/_ENTITY_")]`, gde ćeš _ROLE_ zameniti sa administrator, tourist ili author u zavisnosti od korisnika.
2. Klasa ima privatno polje koje sadrži interfejs servisa, koje dobija putem konstruktora.
3. Klasa definiše jednu ili više metoda koje pozivaju servisne metode i odgovore od servisa vraćaju putem metode `CreateResponse`.
4. Svaka metoda ima odgovarajuću anotaciju za HTTP metodu i dodatnu URL putanju.

**Primer**: Kontrolerska klasa [EquipmentController.cs](https://github.com/psw-ftn/tourism-be/blob/32a7e23909158c6970047f308fbaad62804b6103/src/Explorer.API/Controllers/Administrator/Administration/EquipmentController.cs) iz početnog projekta.

<br/><br/><br/><br/><br/><br/>
## 4. Konfigurisanje skladištenja podataka
Skladištenje podataka je odgovornost koja se rešava u `Infrastructure` projektu povezanog modula. Potrebno je da:

<ol type="a">
  <li>Definišeš DbSet za novi entitet.</li>
  <li>Definišeš novi repozitorijum ako ne koristiš CrudService.</li>
</ol>

### a. Proširivanje DbSeta
Svaki modul ima `DbContext` klasu u okviru `Infrastructure/Database` direktorijuma (npr. `ToursContext.cs`). Pri vrhu ove klase se nalazi linija koda poput `public DbSet<Equipment> Equipment { get; set; }`. Ova linija koda omogućava migracijama da kreiraju tabelu u bazi koja se zove `Equipment` i koja sadrži kolone spram polja `Equipment` klase. Dalje, putem ovog polja možemo da pristupimo sadržaju tabele.

Kada dodajemo novi entitet, potrebno je da dodamo liniju koda u odgovarajuću Context klasu. Ta linija koda će imati oblik `public DbSet<_ENTITY_> _ENTITY_NAME_PLURAL_ { get; set; }` (npr. `public DbSet<User> Users { get; set; }`).

Da bi se nova tabela registrovala, potrebno je da obrišemo stare migracije iz svakog modula (u `Infrastructure` projektu ćemo imati `Migrations` direktorijum koji ceo brišemo) i da obrišemo sve šeme baze podataka (u pgAdminu desni klik na šemu -> Drop Cascade). Zatim ćemo ponoviti korake 0.b. i 0.c. iz ovog dokumenta. Alternativa je da ručno napravimo tabelu putem pgAdmin aplikacije i da ne pokrećemo migracije, što je brže rešenje kada dodajemo jednostavnu tabelu (ili pravimo sitnu izmenu postojeće).

### b. Definisanje repozitorijuma
U situacijama kada nam nije dovoljan CRUD repozitorijum (što neće biti slučaj u prvoj nedelji), možemo da napravimo našu implementaciju repozitorijuma. U tom slučaju treba da:

1. Definišeš interfejs repozitorijuma u okviru `Core` projekta povezanog modula, direktorijum `Domain/RepositoryInterfaces`.
2. Definišeš implementaciju interfejsa repozitorijuma u okviru `Infrastructure` projekta, direktorijum `Database/Repositories`.
3. Navedeš u servisu koji će koristiti dati repozitorijum interfejs repozitorijuma kao parametar konstruktora.

<br/><br/><br/><br/><br/><br/>
## 5. Ažuriranje mehanizma za ubrizgavanje zavisnosti
Svaki modul rešava *dependency injection* u okviru svog `Infrastructure` projekta. Tamo se nalazi `Startup` klasa (npr. `ToursStartup`) koja sadrži dve bitne metode `SetupCore` i `SetupInfrastructure`.

`SetupCore` definiše koje klase iz `Core` projekta treba ubrizgati na mestu kojih interfejsa. `SetupInfrastructure` isto radi, samo za klase koje su implementirane u okviru `Infrastructure` projekta.

**Primer**: [ToursStartup.cs](https://github.com/psw-ftn/tourism-be/blob/32e92f2f6f42094ff89aae6a90aaf25cb0780f1d/src/Modules/Tours/Explorer.Tours.Infrastructure/ToursStartup.cs#L24-L31) sadrži primer kako se definiše *dependency injection* za servise i kako za CRUD repozitorijum.
<br/><br/><br/><br/><br/><br/>
## 6. Kreiranje automatskog testa
TODO
