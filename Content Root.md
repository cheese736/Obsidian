
The content root is the base path for:

- The executable hosting the app (_.exe_).
- Compiled assemblies that make up the app (_.dll_).
- Content files used by the app, such as:
    - Razor files (`.cshtml`, `.razor`)
    - Configuration files (`.json`, `.xml`)
    - Data files (`.db`)
- The [[Web Root]], typically the _wwwroot_ folder.

During development, the content root defaults to the project's root directory. This directory is also the base path for both the app's content files and the [Web root](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-7.0&tabs=windows#web-root). Specify a different content root by setting its path when [building the host](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-7.0&tabs=windows#host). For more information, see [Content root](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-7.0#contentroot).