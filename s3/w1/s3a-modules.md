TODO

## 1. Creating the module subdirectory
First we create a subdirectory with a descriptive name that defines the module. Inside the subdirectory we define the following C# projects:
1. `Tutor.MODULE_NAME.API` class library. The project has a dependency on `Tutor.BuildingBlocks.Core`.
2. `Tutor.MODULE_NAME.Core` class library. The project has a dependency on `Tutor.MODULE_NAME.API`.
3. `Tutor.MODULE_NAME.Infrastructure` class library. The project has a dependency on `Tutor.MODULE_NAME.Core` and `Tutor.BuildingBlocks.Infrastructure`.
4. `Tutor.MODULE_NAME.Tests` xUnit test project. The project has a dependency on `Tutor.API` and `Tutor.BuildingBlocks.Tests`.

[Optional] We can merge projects 1, 2, and 3 into a single class library for modules with simple domain models and supported functionality.

## 2. Populating `Tutor.MODULE_NAME.API`
This project defines interfaces for services supported by the module and the DTO classes that are accepted or returned by these interfaces. Inside the project we define the following directories:
1. `Dtos` contains the DTO class definitions.
2. `Interfaces` contains subdirectories that group interface definitions. Each subdirectory is named after a group of use cases supported by the module.

[Optional] We can further segregate the `Dtos` directory When a module has a complex domain model and many DTO classes. The subdirectory names will likely match the subdirectories in `Tutor.MODULE_NAME.Core/Domain` directory.

## 3. Populating `Tutor.MODULE_NAME.Core`
This project defines service implementations and the module's domain model. Inside the project we define the following directories:
1. `Domain` contains classes that make up the domain model. It includes a subdirectory named `RepositoryInterfaces`.
2. `Mappers` contains `AutoMapper` profile definitions used to map domain model objects to DTOs and vice-versa.
3. `UseCases` contains subdirectories that group service interface implementations. Each subdirectory is named after a group of use cases supported by the module. Here we also define the `IMODULE_NAMEUnitOfWork.cs` interface with the following minimal code: `public interface IMODULE_NAMEUnitOfWork : IUnitOfWork {}`

[Optional] We introduce subdirectories to the `Domain` directory when the module's domain is complex and can be segregated into logical units (e.g., aggregates).

[Optional] We define interfaces for infrastructure services next to use case services when the service requires a non-repository infrastructure service. If more than one use case group requires an infrastructure service, we define the `InfrastructureInterfaces` subdirectory in the `UseCases` directory.

## 4. Populating `Tutor.MODULE_NAME.Infrastructure`
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

## 5. Expanding `Tutor.API`
With the module set up, there are two additional steps that tie the module into the complete solution:
1. The `Tutor.API` project needs to reference `Tutor.MODULE_NAME.API` so that the controllers can contact the module's services. The project also needs to reference `Tutor.MODULE_NAME.Infrastructure` to access the Setup class.
2. Expand the sole method in the `Startup/ModulesConfiguration.cs` class to include the line `services.ConfigureMODULE_NAMEModule();`.

## 6. Populating `Tutor.MODULE_NAME.Tests`
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

The final step entails registering the new module with the `Tutor.Architecture.Tests` tests. This includes finding the `ModuleTests.cs` file and adding the module name at the very end of the file, following the pattern used for other modules.

With this step complete the module is integrated to the Tutor modular monolith.

Remember, when in doubt, consult the code of existing modules.
