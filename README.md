# Get started with [ASP.NET][asp_net] Core MVC

This repository follows the steps in the ["Get started with ASP.NET Core MVC"][get_started_with_asp_net_core_mvc] guide by Microsoft.

## Prerequisites

- [Visual Studio Code][vs_code]
- [Lastest Version of .NET Core SDK][dotnet_core_sdk]

## Create a Web App

- Open the integrated terminal.
- Change directories to a folder which will contain the project.
- Run `dotnet new mvc -o MvcMovie`
- Run `code -r MvcMovie`

- A dialog box will appear with the message:
    > **Required assets to build and debug are missing from 'MvcMovie'. Add them?**
- Select **Yes**.

## Run the App

- Press `CTRL+F5` to run without the debugger.
- Run `dotnet dev-certs https --trust` to trust the https development certificate. (Does not work on Linux.)
- Select **Yes** in the dialog box that pops up.

Visual Studio Code will launch a browser and navigate to https://localhost:5001.

By launching the app in non-debug mode changes can be made to the code and the changes can be viewed by simply refreshing the browser.

## Add a Controller

- Right click the Controllers folder and select New File
- Name the new file `HelloWorldController.cs`
- Replace the contents of the new file with:
    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace MvcMovie.Controllers
    {
        public class HelloWorldController : Controller
        {
            // 
            // GET: /HelloWorld/

            public string Index()
            {
                return "This is my default action...";
            }

            // 
            // GET: /HelloWorld/Welcome/ 

            public string Welcome()
            {
                return "This is the Welcome action method...";
            }
        }
    }
    ```
- Run the app in non-debug mode and append "/HelloWorld" to the address bar path.
- Append "/Welcome" to the address bar path.

### Add Parameters to the Controller

- Modify the welcome method to pass some parameter information from the URL to the controller:
    ```csharp
    // GET: /HelloWorld/Welcome/ 
    // Requires using System.Text.Encodings.Web;
    public string Welcome(string name, int numTimes = 1)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, NumTimes is: {numTimes}");
    }
    ```
- Run the app in non-debug mode.
- Append "?name=Rick&numtimes=4" to the address bar path.

### Add Optional Parameters to the Controller

- Modify the Welcome method to the following code:
    ```csharp
    public string Welcome(string name, int ID = 1)
    {
        return HtmlEncoder.Default.Encode($"Hello {name}, ID: {ID}");
    }
    ```
- Run the app in non-debug mode.
- Change the route parameter to "/3?name=Rick"

## Add a View

- Replace the `Index` method in the `HelloWorldController` with the following code:
    ```csharp
    public IActionResult Index()
    {
        return View();
    }
    ```
- Add a new folder named `Views/HelloWorld`.
- Add a new file to the `Views/HelloWorld` folder named `Index.cshtml`.
- Replace the contents of the `Index.cshtml` file with:
    ```html
    @{
        ViewData["Title"] = "Index";
    }

    <h2>Index</h2>

    <p>Hello from our View Template!</p>
    ```
- Run the app in non-debug mode.
- Append `/HelloWorld` to the address path.

### Change Views and Layout Pages

- Replace the content of the `Views/SHared/_Layout.cshtml` file with the following:
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>@ViewData["Title"] - Movie App</title>
        <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />
        <link rel="stylesheet" href="~/css/site.css" />
    </head>
    <body>
        <header>
            <nav class="navbar navbar-expand-sm navbar-toggleable-sm navbar-light bg-white border-bottom box-shadow mb-3">
                <div class="container">
                    <a class="navbar-brand" asp-controller="Movies" asp-action="Index">Movie App</a>
                    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target=".navbar-collapse" aria-controls="navbarSupportedContent"
                            aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>
                    <div class="navbar-collapse collapse d-sm-inline-flex flex-sm-row-reverse">
                        <ul class="navbar-nav flex-grow-1">
                            <li class="nav-item">
                                <a class="nav-link text-dark" asp-area="" asp-controller="Home" asp-action="Index">Home</a>
                            </li>
                            <li class="nav-item">
                                <a class="nav-link text-dark" asp-area="" asp-controller="Home" asp-action="Privacy">Privacy</a>
                            </li>
                        </ul>
                    </div>
                </div>
            </nav>
        </header>
        <div class="container">
            <main role="main" class="pb-3">
                @RenderBody()
            </main>
        </div>

        <footer class="border-top footer text-muted">
            <div class="container">
                &copy; 2020 - Movie App - <a asp-area="" asp-controller="Home" asp-action="Privacy">Privacy</a>
            </div>
        </footer>
        <script src="~/lib/jquery/dist/jquery.min.js"></script>
        <script src="~/lib/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
        <script src="~/js/site.js" asp-append-version="true"></script>
        @RenderSection("Scripts", required: false)
    </body>
    </html>
    ```
- Change the title and `<h2>` element of the `Views/HelloWorld/Index.cshtml` view file.
    ```html
    @{
        ViewData["Title"] = "Movie List";
    }

    <h2>My Movie List</h2>

    <p>Hello from our View Template!</p>
    ```
- Run the app in non-debug mode.
- Append `/HelloWorld` to the address bar path.

### Passing Data from the Controller to the View

- Change the code in the `HelloWorldController` to the following:
    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using System.Text.Encodings.Web;

    namespace MvcMovie.Controllers
    {
        public class HelloWorldController : Controller
        {
            public IActionResult Index()
            {
                return View();
            }

            public IActionResult Welcome(string name, int numTimes = 1)
            {
                ViewData["Message"] = "Hello " + name;
                ViewData["NumTimes"] = numTimes;

                return View();
            }
        }
    }
    ```
- Create a view template file `Views/HelloWorld/Welcome.cshtml` with the following code:
    ```html
    @{
        ViewData["Title"] = "Welcome";
    }

    <h2>Welcome</h2>

    <ul>
        @for (int i = 0; i < (int)ViewData["NumTimes"]; i++)
        {
            <li>@ViewData["Message"]</li>
        }
    </ul>
    ```
- Run the app in non-debug mode.
- Append `/HelloWorld/Welcome?name=Rick&numtimes=4` to the address bar path.


[asp_net]: <https://dotnet.microsoft.com/apps/aspnet> "ASP.NET"
[dotnet_core_sdk]: <https://dotnet.microsoft.com/download>
[get_started_with_asp_net_core_mvc]: <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1&tabs=visual-studio-code> "Get started with ASP.NET Core MVC"
[vs_code]: <https://code.visualstudio.com/Download> "Visual Studio Code"