TODO: Istakni šta će biti novi moduli i onda proces. (u našem slučaju `Payments` i `Encounters`)

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

## 4. Populating `Explorer.MODULE_NAME.Infrastructure`
This project defines repository and other infrastructure services implementations. Inside the project we define the following directories and classes:
1. `Database` contains the following:
   1. `MODULE_NAMEContext.cs` class definition, which inherits `DbContext`, defines `DbSet`s for each domain entity, and overrides `OnModelCreating`. At a minimum, the `OnModelCreating` should include the following line of code: `modelBuilder.HasDefaultSchema(MODULE_NAME);`. The schema name should be `camelCase`.
   2. `MODULE_NAMEUnitOfWork.cs` class definition, with the following code:
      ```csharp
      public class MODULE_NAMEUnitOfWork : UnitOfWork<MODULE_NAMEContext>, IMODULE_NAMEUnitOfWork
      {
          public MODULE_NAMEUnitOfWork(MODULE_NAMEContext dbContext) : base(dbContext) {}
      }
      ```
   3. `Repositories` directory that includes repository interface implementations.
2. `MODULE_NAMEStartup.cs` defines the module's dependency injection and service configuration. At a minimum, it should include the following method:
   ```csharp
   public static IServiceCollection ConfigureMODULE_NAMEModule(this IServiceCollection services)
   {
       services.AddAutoMapper(typeof(MODULEProfile).Assembly);
       SetupCore(services);
       SetupInfrastructure(services);
       return services;
   }
   ```
   where the first line sets up AutoMapper profiles (one profile should be listed even if multiple profiles exist as the code references the assembly), `SetupCore` adds scoped service implementations to the related interfaces, and `SetupInfrastructure` adds scoped repository implementations for the related interfaces, DbContext, and any additional infrastructure service configurations.

[Optional] We define a new directory when a module requires additional infrastructure services (e.g., email client, HTTP connection).

## 5. Expanding `Explorer.API`
With the module set up, there are two additional steps that tie the module into the complete solution:
1. The `Explorer.API` project needs to reference `Explorer.MODULE_NAME.API` so that the controllers can contact the module's services. The project also needs to reference `Explorer.MODULE_NAME.Infrastructure` to access the Setup class.
2. Expand the sole method in the `Startup/ModulesConfiguration.cs` class to include the line `services.ConfigureMODULE_NAMEModule();`.

## 6. Populating `Explorer.MODULE_NAME.Tests`
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
