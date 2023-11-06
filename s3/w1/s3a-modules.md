TODO: Istakni šta će biti novi moduli i onda proces. (u našem slučaju `Payments` i `Encounters`)
TODO: Veće grupe slučajeva korišćenja definiši.

## 1. Kreiranje projekata za novi modul
Na početku je potrebno napraviti novi direktorijum u okviru `Modules` koji nosi naziv novog modula. U okviru tog direktorijuma definišemo sledeće projekte:
1. `Explorer.MODULE_NAME.API` class library. Ovaj projekat referencira `Explorer.BuildingBlocks.Core` (desni klik na projekat, `Add > Project Reference`).
2. `Explorer.MODULE_NAME.Core` class library. Ovaj projekat referencira `Explorer.MODULE_NAME.API`.
3. `Explorer.MODULE_NAME.Infrastructure` class library. Ovaj projekat referencira `Explorer.MODULE_NAME.Core` i `Explorer.BuildingBlocks.Infrastructure`.
4. `Explorer.MODULE_NAME.Tests` xUnit test project. Ovaj projekat referencira `Explorer.API` i `Explorer.BuildingBlocks.Tests`.

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

## 6. Popunjavanje `Explorer.MODULE_NAME.Tests`
This project defines automated tests. Inside the project we define the following directories and classes:
1. `Integration` contains subdirectories for each use case group supported by the module. The subdirectories contain integration test classes.
2. `TestData` contains sql scripts required to setup the test database.
3. `MODULE_NAMETestFactory.cs` defines a simple class that inherits `BaseTestFactory<MODULE_NAMEContext>` and implements the `ReplaceNeededDbContexts` method. This method should redefine all DbContexts the module relies on (i.e., its DbContext and the DbContext of modules that it contacts). The code below illustrates how this can be achieved:
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
   4. `BaseMODULE_NAMEIntegrationTest.cs` defines a simple class that inherits `BaseWebIntegrationTest<MODULE_NAMETestFactory>` and defines an empty constructor. This class is inherited by all integration tests in this module.

The final step entails registering the new module with the `Explorer.Architecture.Tests` tests. This includes finding the `ModuleTests.cs` file and adding the module name at the very end of the file, following the pattern used for other modules.

With this step complete the module is integrated to the Explorer modular monolith.

Remember, when in doubt, consult the code of existing modules.
