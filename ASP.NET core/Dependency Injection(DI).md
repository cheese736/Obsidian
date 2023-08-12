ASP.NET Core supports the dependency injection (DI) software design pattern, which is a technique for achieving [Inversion of Control (IoC)](https://learn.microsoft.com/en-us/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) between classes and their dependencies.

>A _dependency_ is an object that another object depends on.

Examine the following `MessageWriter` class with a `Write` method that other classes depend on:

```C#
public class MessageWriter
{
    public void Write(string message)
    {
        Console.WriteLine($"MessageWriter.Write(message: \"{message}\")");
    }
}

public class Worker : BackgroundService
{
    private readonly MessageWriter _messageWriter = new MessageWriter();

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _messageWriter.Write($"Worker running at: {DateTimeOffset.Now}");
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

The class creates and directly depends on the `MessageWriter` class. Hard-coded dependencies, such as in the previous example, are problematic and should be avoided for the following reasons:

- To replace `MessageWriter` with a different implementation, the `Worker` class must be modified.
- If `MessageWriter` has dependencies, they must also be configured by the `Worker` class. In a large project with multiple classes depending on `MessageWriter`, the configuration code becomes scattered across the app.
- This implementation is difficult to unit test. The app should use a mock or stub `MessageWriter` class, which isn't possible with this approach.

Dependency injection addresses these problems through:

- The use of an interface or base class to abstract the dependency implementation.
   
- Registration of the dependency in a ==service container.== .NET provides a built-in service container, [IServiceProvider](https://learn.microsoft.com/en-us/dotnet/api/system.iserviceprovider). Services are typically registered at the app's start-up and appended to an [IServiceCollection](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection). Once all services are added, you use [BuildServiceProvider](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectioncontainerbuilderextensions.buildserviceprovider) to create the service container.
  
- _Injection_ of the service into the constructor of the class where it's used. ==The framework takes on the responsibility of creating an instance of the dependency and disposing of it when it's no longer needed.==

As an example, the `IMessageWriter` interface defines the `Write` method:
```C#

namespace DependencyInjection.Example;

public interface IMessageWriter
{
    void Write(string message);
}

public class MessageWriter : IMessageWriter
{
    public void Write(string message)
    {
        Console.WriteLine($"MessageWriter.Write(message: \"{message}\")");
    }
}

```

The sample code registers the `IMessageWriter` service with the concrete type `MessageWriter`. The [AddScoped](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addscoped) method registers the service with a scoped lifetime, the lifetime of a single request.

ref: [Service lifetimes](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-7.0#service-lifetimes) [[Service lifetimes]]

```c#

using DependencyInjection.Example;

HostApplicationBuilder builder = Host.CreateApplicationBuilder(args);

builder.Services.AddHostedService<Worker>();
builder.Services.AddSingleton<IMessageWriter, MessageWriter>();

using IHost host = builder.Build();

host.Run();

```

In the preceding code, the sample app:

- Creates a host app builder instance.
    
- Configures the services by registering:
    - The `Worker` as a hosted service. For more information, see [Worker Services in .NET](https://learn.microsoft.com/en-us/dotnet/core/extensions/workers).
    - The `IMessageWriter` interface as a singleton service with a corresponding implementation of the `MessageWriter` class.
      
- Builds the host and runs it.

The host contains the dependency injection service provider. It also contains all the other relevant services required to automatically instantiate the `Worker` and provide the corresponding `IMessageWriter` implementation as an argument.

```C#
namespace DependencyInjection.Example;

public sealed class Worker : BackgroundService
{
    private readonly IMessageWriter _messageWriter;

    public Worker(IMessageWriter messageWriter) =>
        _messageWriter = messageWriter;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _messageWriter.Write($"Worker running at: {DateTimeOffset.Now}");
            await Task.Delay(1_000, stoppingToken);
        }
    }
}

```

By using the DI pattern, the worker service:

- Doesn't use the concrete type `MessageWriter`, only the `IMessageWriter` interface that implements it. That makes it easy to change the implementation that the worker service uses without modifying the worker service.
  
- Doesn't create an instance of `MessageWriter`. The instance is created by the DI container.

It's not unusual to use dependency injection in a chained fashion. Each requested dependency in turn requests its own dependencies. The container resolves the dependencies in the graph and returns the fully resolved service. The collective set of dependencies that must be resolved is typically referred to as a _dependency tree_, _dependency graph_, or _object graph_.

The container resolves `ILogger<TCategoryName>` by taking advantage of [(generic) open types](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/types#843-open-and-closed-types), eliminating the need to register every [(generic) constructed type](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/types#84-constructed-types).

With dependency injection terminology, a service:

- Is typically an object that provides a service to other objects, such as the `IMessageWriter` service.
- Is not related to a web service, although the service may use a web service.

The framework provides a robust logging system. The `IMessageWriter` implementations shown in the preceding examples were written to demonstrate basic DI, not to implement logging. Most apps shouldn't need to write loggers.