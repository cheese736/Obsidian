## The DbContext lifetime

The lifetime of a `DbContext` begins when the instance is created and ends when the instance is [disposed](https://learn.microsoft.com/en-us/dotnet/standard/garbage-collection/unmanaged). A `DbContext` instance is designed to be used for a _single_ [unit-of-work](https://www.martinfowler.com/eaaCatalog/unitOfWork.html). This means that the lifetime of a `DbContext` instance is usually very short.

A typical unit-of-work when using Entity Framework Core (EF Core) involves:

- Creation of a `DbContext` instance
- Tracking of entity instances by the context. Entities become tracked by
    - Being [returned from a query](https://learn.microsoft.com/en-us/ef/core/querying/tracking)
    - Being [added or attached to the context](https://learn.microsoft.com/en-us/ef/core/saving/disconnected-entities)
- Changes are made to the tracked entities as needed to implement the business rule
- [SaveChanges](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechanges) or [SaveChangesAsync](https://learn.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.savechangesasync) is called. EF Core detects the changes made and writes them to the database.
- The `DbContext` instance is disposed

## DbContext in dependency injection for ASP.NET Core

In many web applications, each HTTP request corresponds to a single unit-of-work. This makes tying the context lifetime to that of the request a good default for web applications.

ASP.NET Core applications are [configured using dependency injection](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup). EF Core can be added to this configuration using [AddDbContext](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontext) in the [`ConfigureServices`](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/startup#the-configureservices-method) method of `Startup.cs`. For example:

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddControllers();

    services.AddDbContext<ApplicationDbContext>(
        options => options.UseSqlServer("name=ConnectionStrings:DefaultConnection"));
}
```