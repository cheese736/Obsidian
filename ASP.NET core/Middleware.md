The request handling pipeline is composed as a series of middleware components. 
==Each component performs operations on an [`HttpContext`](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/http-context?view=aspnetcore-7.0) and either invokes the next middleware in the pipeline or terminates the request.==

![[Pasted image 20230811020647.png]]


By convention, a middleware component is added to the pipeline by invoking a `Use{Feature}` extension method.

```C#

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.AddControllersWithViews();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseAuthorization();

app.MapGet("/hi", () => "Hello!");

app.MapDefaultControllerRoute();
app.MapRazorPages();

app.Run();
```