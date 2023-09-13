The web root is the base path for public, static resource files, such as:

- Stylesheets (`.css`)
- JavaScript (`.js`)
- Images (`.png`, `.jpg`)

By default, static files are served only from the web root directory and its sub-directories. The web root path defaults to _{content root}/wwwroot_. Specify a different web root by setting its path when [building the host](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-7.0&tabs=windows#host). For more information, see [Web root](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-7.0#webroot).

Prevent publishing files in _wwwroot_ with the [`<Content> project item`](https://learn.microsoft.com/en-us/visualstudio/msbuild/common-msbuild-project-items#content) in the project file. The following example prevents publishing content in _wwwroot/local_ and its sub-directories:

``` XML
<ItemGroup>
  <Content Update="wwwroot\local\**\*.*" CopyToPublishDirectory="Never" />
</ItemGroup>

```

In Razor `.cshtml` files, `~/` points to the web root. A path beginning with `~/` is referred to as a _virtual path_.

For more information, see [Static files in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/static-files?view=aspnetcore-7.0).