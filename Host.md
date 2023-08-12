On startup, an ASP.NET Core app builds a _host_. The host encapsulates all of the app's resources, such as:

- An HTTP server implementation
- Middleware components
- Logging
- Dependency injection (DI) services
- Configuration

There are three different hosts capable of running an ASP.NET Core app:

- [ASP.NET Core WebApplication](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/webapplication?view=aspnetcore-7.0), also known as the [Minimal Host](https://learn.microsoft.com/en-us/aspnet/core/migration/50-to-60?view=aspnetcore-7.0#new-hosting-model)
- [.NET Generic Host](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-7.0) combined with ASP.NET Core's [ConfigureWebHostDefaults](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.hosting.generichostbuilderextensions.configurewebhostdefaults)
- [ASP.NET Core WebHost](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/web-host?view=aspnetcore-7.0)

The ASP.NET Core [WebApplication](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplication) and [WebApplicationBuilder](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder) types are recommended and used in all the ASP.NET Core templates. `WebApplication` behaves similarly to the .NET Generic Host and exposes many of the same interfaces but requires less callbacks to configure. The ASP.NET Core [WebHost](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.webhost) is available only for backward compatibility.

The following example instantiates a `WebApplication`:

```C#

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();
```

The [WebApplicationBuilder.Build](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder.build) method configures a host with a set of default options, such as:

- Use [Kestrel](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-7.0&tabs=windows#servers) as the web server and enable IIS integration.
- Load [configuration](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-7.0) from `appsettings.json`, environment variables, command line arguments, and other configuration sources.
- Send logging output to the console and debug providers.