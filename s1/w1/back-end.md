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
  <li>Kako da napišemo automatski test koji proverava da sve radi.</li>
</ol>

## 0. Organizacija i pokretanje projekta
Prvi put kad sedneš da radiš na projektu ćeš morati da kloniraš repozitorijum svog tima na svoju mašinu. Ovde će ti pomoći `git clone` komanda uz URL repozitorijuma tima.

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
Prethodna komanda će u svakom `Infrastructure` projektu da generiše datoteke i da napravi potrebne tabele u bazi.

## 1. Kreiranje domenske klase
TODO

## 2. Kreiranje servisa modula
TODO

## 3. Kreiranje kontrolera
TODO

## 4. Kreiranje repozitorijuma
TODO

## 5. Kreiranje automatskog testa
TODO
