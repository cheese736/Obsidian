
An ASP.NET Core app uses an HTTP server implementation to listen for HTTP requests. The server surfaces requests to the app as a set of [request features](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/request-features?view=aspnetcore-7.0) composed into an `HttpContext`.

Windows

ASP.NET Core provides the following server implementations:

- _Kestrel_ is a cross-platform web server. Kestrel is often run in a reverse proxy configuration using [IIS](https://www.iis.net/). In ASP.NET Core 2.0 or later, Kestrel can be run as a public-facing edge server exposed directly to the Internet.
- _IIS HTTP Server_ is a server for Windows that uses IIS. With this server, the ASP.NET Core app and IIS run in the same process.
- _HTTP.sys_ is a server for Windows that isn't used with IIS.