Serverski deo aplikacije je izgrađen koristeći:

- ASP.NET radni okvir za izgradnju Web aplikacije,
- *Entity Framework* biblioteku za objektno-relaciono mapiranje (pretvaranje objekata u redove SQL tabela i obratno),
- *AutoMapper* biblioteke za pretvaranje DTO instanci u domenske objekte i obratno,
- *xUnit* radni okvir za pisanje automatskih testova.
- *PostgreSQL* bazu podataka.

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
Prvi put kad sedneš da radiš na projektu ćeš morati da kloniraš repozitorijum svog tima lokalno. Ovde će ti pomoći `git clone` komanda uz URL repozitorijuma tima.

Solution koji učitaš u razvojno okruženje (naša preporuka je Visual Studio) se sastoji od više projekata i paketa. Prvа celina sadrži gradivne elemente celokupnog projekta koji ćeš ostatak koda koristiti:
```
BuildingBlocks                                   - Sadrži common klase, odnosno klase koje su korisne svim modulima od modularnog monolita.
  -> Explorer.BuildingBlocks.Core                - Klase koje su korisne svim API i Core projektima.
  -> Explorer.BuildingBlocks.Infrastructure      - Klase koje su korisne Infrastructure projektima.
  -> Explorer.BuildingBlocks.Tests               - Klase koje su korisne Tests projektima.
```
BuildingBlocks paket će se retko menjati tokom kursa i ne treba da ga diramo u prvom sprintu.

Većina izmena će se dešavati u različitim modulima našeg modularnog monolita:
```
Modules                                          - Sadrži sve module (package-by-feature) od modularnog monolita.
  -> Blog                                        - Modul koji se bavi funkcionalnostima vezanim za Blog.
    -> Explorer.Blog.API                         - API projekat definiše interfejse modula koje će implementirati servisne klase u Core projektu. Uz to definiše i  DTO klase modula.
    -> Explorer.Blog.Core                        - Core projekat sadrži domenski i servisni sloj. Ovo je jedino mesto gde ćemo imati poslovnu logiku i većinu želimo da postavimo upravo u domenski sloj.
    -> Explorer.Blog.Infrastructure              - Infrastructure projekat sadrži repozitorijume i ostale infrastrukturne servise koje ćemo vremenom dodavati u projekat.
    -> Explorer.Blog.Tests                       - Tests projekat sadrži automatske testove koji proveravaju da li je naš kod ispravan.
  -> Stakeholders                                - Modul koji se bavi funkcionalnostima vezanim za registraciju korisničkih profila i komunikacijom između njih
    -> ...
  -> Tours                                       - Modul koji se bavi funkcionalnostima vezanim za prodaju i izvršavanje tura
    -> ...
```
U startu ćemo imati 3 modula, a kako projekat bude rastao ćemo dodati još. Na kraju vidimo još dva projekta:
```
Explorer.API                                     - Definiše kontrolerske klase koje se aktiviraju uz pomoć HTTP zahteva koji nam stižu sa Angular aplikacije.
Explorer.Architecture.Tests                      - Definiše automatske testove koji proveravaju da li je naša arhitektura i dalje ispravna.
```
Explorer.API projekat ćemo proširivati kada god želimo da ponudimo novu funkciju klijentskoj aplikaciji. Explorer.Architecture.Tests projekat nećemo nikad dirati, već ćemo koristiti ove testove da ispratimo da li je arhitektura ispoštovana.

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
