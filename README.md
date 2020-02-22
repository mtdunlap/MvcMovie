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


[asp_net]: <https://dotnet.microsoft.com/apps/aspnet> "ASP.NET"
[dotnet_core_sdk]: <https://dotnet.microsoft.com/download>
[get_started_with_asp_net_core_mvc]: <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1&tabs=visual-studio-code> "Get started with ASP.NET Core MVC"
[vs_code]: <https://code.visualstudio.com/Download> "Visual Studio Code"