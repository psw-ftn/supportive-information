Uvodimo dva nova modula kako bismo odgovorili na zahteve koje uvodimo tokom preostala dva sprinta:

- U okviru `Payments` modula definišemo domenske objekte i funkcionalnosti vezane za problem prodaje i plaćanja. Ovde ćemo smestiti funkcionalnosti vezane za ShoppingCart, istoriju prodaja, kupone i ostale koncepte koji se tiču čina kupovine i prodaje bez obzira na to šta se prodaje.
- U okviru `Encounters` modula uvodimo eksperimentalne funkcionalnosti koje se tiču turizma i omogućavaju dodatne vrste događaja koji će angažovati turiste i privući ih da koriste našu aplikaciju.

Da bismo uveli nove module i zaokružili zadatak, potrebno je za svaki modul da:

- Kreiramo početne projekte modula i postavimo početne direktorijume i klase za svaki projekat.
- Uvežemo novi modul sa `Explorer.API`.
- Implementiramo jednostavnu funkcionalnost za svaki novi modul.

## 1. Kreiranje projekata za novi modul
Na početku je potrebno napraviti novi direktorijum u okviru `Modules` koji nosi naziv novog modula. U okviru tog direktorijuma definišemo sledeće projekte:

1. `Explorer.MODULE_NAME.API` class library. Ovaj projekat referencira `Explorer.BuildingBlocks.Core` (desni klik na projekat, `Add > Project Reference`).
2. `Explorer.MODULE_NAME.Core` class library. Ovaj projekat referencira `Explorer.MODULE_NAME.API`.
3. `Explorer.MODULE_NAME.Infrastructure` class library. Ovaj projekat referencira `Explorer.MODULE_NAME.Core` i `Explorer.BuildingBlocks.Infrastructure`.
4. `Explorer.MODULE_NAME.Tests` xUnit test project. Ovaj projekat referencira `Explorer.API` i `Explorer.BuildingBlocks.Tests`.

**Napomena**: Ako u bilo kom momentu nije jasno šta treba uraditi, konsultujte [module u početnom projektu](https://github.com/psw-ftn/tourism-be/tree/main/src/Modules/Stakeholders).

## 2. Popunjavanje `Explorer.MODULE_NAME.API`
Projekat definiše interfejse servisa koje modul podržava i DTO klase koje interfejsi prihvataju i vraćaju. U okviru projekta definišemo direktorijume:

1. `Dtos` sadrži definicije DTO klasa. Po potrebi se segmentira na poddirektorijume koji grupiše povezane DTO klase (npr. po uzoru na grupisanje u `Core/Domain`).
2. `Public` sadrži interfejse javnih servise modula (ove interfejse pozivaju kontroleri). Po potrebi se segmentira na poddirektorijume koji grupišu interfejse servisa spram povezanih slučajeva korišćenja.
3. `Internal` sadrži interfejse servisa modula koje pozivaju drugi moduli (ove interfejse pozivaju servisi drugih modula).

## 3. Popunjavanje `Explorer.MODULE_NAME.Core`
Projekat definiše implementacije servisa, domenski model i profile za mapiranje domenskog modela na DTO klase. U okviru projekta definišemo direktorijume:

1. `Domain` sadrži klase domenskog modela i interfejse repozitorijuma. Po potrebi se segmentira na poddirektorijume koji odgovaraju agregatima.
2. `Mappers` sadrži `AutoMapper` definicije profila.
3. `UseCases` sadrži implementacije servisa modula. Po potrebi se segmentira na poddirektorijume, gde svaki odgovara većem skupu povezanih slučajeva korišćenja.

## 4. Popunjavanje `Explorer.MODULE_NAME.Infrastructure`
Projekat definiše implementacije servisa, domenski model i profile za mapiranje domenskog modela na DTO klase. U okviru projekta definišemo direktorijume i klase:

1. `Database` direktorijum sadrži:
   1. `MODULE_NAMEContext.cs` definiciju klase. Ova klasa nasleđuje `DbContext`, definiše `DbSet` za svaki entitet, i override-uje `OnModelCreating` metodu. Ova metoda na početku treba da sadrži sledeću liniju koda: `modelBuilder.HasDefaultSchema(MODULE_NAME);`. Naziv šeme prati `camelCase`.
   2. `Repositories` direktorijum sadrži implementacije repository interfejsa.
2. `MODULE_NAMEStartup.cs` definiše _dependency injection_ i ostalu konfiguraciju modulu. Na početku treba da sadrži sledeću metodu:
   ```csharp
   public static IServiceCollection ConfigureMODULE_NAMEModule(this IServiceCollection services)
   {
       services.AddAutoMapper(typeof(MODULEProfile).Assembly);
       SetupCore(services);
       SetupInfrastructure(services);
       return services;
   }
   ```
   gde prva linija metode konfiguriše `AutoMapper` profil (navodimo jedan profil čak i ako ih imamo više; preduslov je da smo definisali takvu klasu u `Core/Mappers`), `SetupCore` određuje *dependency injection* za servise, a `SetupInfrastructure` za repozitorijume, DbContext, i ostale infrastrukturne servise (za sada ih nemamo).

## 5. Proširivanje `Explorer.API`
Ostala su dva koraka kako bismo uvezali nov modul sa kompletnim rešenjem:
1. `Explorer.API` projekat treba da referencira `Explorer.MODULE_NAME.API` da bi kontroleri mogli da kontaktiraju servise modula. Takođe treba da referencira `Explorer.MODULE_NAME.Infrastructure` da pristupi konfiguraciji modula.
2. Potrebno je proširiti jednu liniju koda u okviru metode `Startup/ModulesConfiguration.cs` klase. Dodati liniju koda `services.ConfigureMODULE_NAMEModule();`.

**Napomena**: U buduće će biti potrebno kreirati dodatnu šemu u produkcionoj bazi podataka koja odgovara nazivu šeme za ovaj modul.

## 6. Popunjavanje `Explorer.MODULE_NAME.Tests`
Projekat definiše automatske testove od modula. U okviru projekta definišemo direktorijume i klase:

1. `Integration` sadrži definicije automatskih testova. Po potrebi se segmentira na poddirektorijume za svaku grupu slučajeva korišćenja koje modul podržava.
2. `TestData` sadrži sql scripte potrebne za uspostavljanje testne baze podataka.
3. `MODULE_NAMETestFactory.cs` definiše prostu klasu koja nasleđuje `BaseTestFactory<MODULE_NAMEContext>` i implementira `ReplaceNeededDbContexts` metodu. Ova metoda redefiniše sve DbContext-e koji su potrebni modulu (minimalno DbContext od samog modula, kao i DbContext od svakog modula kog ovaj modul poziva (ako takvih ima)). Sledeći kod ilustruje kako ovo izgleda:
   ```csharp
   protected override IServiceCollection ReplaceNeededDbContexts(IServiceCollection services)
   {
       var descriptor = services.SingleOrDefault(d => d.ServiceType == typeof(DbContextOptions<MODULE_NAMEContext>));
       services.Remove(descriptor!);
       services.AddDbContext<MODULE_NAMEContext>(SetupTestContext());

       descriptor = services.SingleOrDefault(d => d.ServiceType == typeof(DbContextOptions<OTHER_MODULE_NAMEContext>));
       services.Remove(descriptor!);
       services.AddDbContext<OTHER_MODULE_NAMEContext>(SetupTestContext());

       return services;
   }
   ```
4. `BaseMODULE_NAMEIntegrationTest.cs` definiše jednostavnu klasu koja nasleđuje `BaseWebIntegrationTest<MODULE_NAMETestFactory>` i definiše prazan konstruktor. Ovu klasu nasleđuju svi integracioni testovu u okviru ovog modula.

Poslednji korak podrazumeva da se registruje novi modul sa `Explorer.Architecture.Tests` testovima. U okviru tog projekta pronađi `ModuleTests.cs` i dodaj naziv modula u listu na kraju datoteke, prateći šablon za ostale module.

U ovom momentu bi ceo solution trebao da se kompajlira. Ako pokrenemo automatske testove, trebali bismo da vidimo da je proširen broj arhitekturalnih testova koji uključuju i novi modul. Ako sve prolazi, Explorer modularan monolit je proširen novim modulom i možemo da napravimo commit vezan za njegovo uvođenje.

## 7. Dodavanje proste funkcionalnosti u novi modul
Na kraju je potrebno da uvedemo prostu funkcionalnost spram korisničkih priča koje smo dobili za ovaj sprint. Uvođenjem nove funkcije ćemo osigurati da je modul dobro postavljen i da radi u testnim i produkcionim uslovima. Proces uvođenja proste funkcionalnosti odgovara [prvom zadatku sa kursa](https://github.com/psw-ftn/supportive-information/tree/master/s1/w1).
