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


[asp_net]: <https://dotnet.microsoft.com/apps/aspnet> "ASP.NET"
[dotnet_core_sdk]: <https://dotnet.microsoft.com/download>
[get_started_with_asp_net_core_mvc]: <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1&tabs=visual-studio-code> "Get started with ASP.NET Core MVC"
[vs_code]: <https://code.visualstudio.com/Download> "Visual Studio Code"