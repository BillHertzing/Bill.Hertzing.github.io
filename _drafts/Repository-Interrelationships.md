---
Title: Repository Interrelationships
tags: [AceCommander, ATAP.Utilities, Blazor, StronglyTypedIds, BillHertzing Blog]
description: A broad overview of the repositories in my GitHub account, and how they relate toone another
category: technical 
---

An explanation of how my technical repositories relate to one another.

-- add dot diagram here? use a png to start.

I am writing a program that will help you make / string together programs that automate some of your ToDos in real life. The program I'm writing runs anywhere .Net Core 3.0 runs, uses a Blazor interface, supports a bare minimum "I'm here" in minimal mode, but can be expanded by the enabling of features and loading of PlugIns. PlugIns are designed to share their public data, methods and events with each other.

I'm also publishing a series of Demo programs that explain in detail the concepts and constructs used in the AceCommander program. This is ensure I understand, and can explain, what 'the code I got from goggling the Internet' is doing when I use it. The Demos are also another way I want to give back and help others understand how the C# language and the .Net  libraries can be used.

The software in these repositoies are an ongoing effort to collect in a centralized location data structures, algorithms an concepts that I've developed or used over the coursse of 45 years of working with computers.

One repository is called Ace. Ace is my take on the implementation of a digital assistant. Doing a search on GitHub for "Jarvis" (The English accented AI personal assistant to Tony Stark in the Ironman movies) results in hundreds of repositories bearing vriations on that name, and a quick browse through some of them reveals that the desire to code up our won JArvis appeals to many programmers.

Ace is designed to be availalble on any kind of device. The primary/initial implemenations are on Windows and Linux. The software is designed to be a Windows Service or a Linux Demon. The base implemention provides a simple shell of basic services, and a framework for adding plugins. Most of Ace's features and capabilities are provided by individual plugins.

Ace is built on Dot Net components. The framework is primarly DotNet standard (curretnly an V2.1) for the majority of code, since this code will run on both Linux and Windows. The full Windows framework modules (currently DotNet471) is used for the Windows-Service specific portions; DotNetCore is used for the Linux runtime daemon.

The Windows-Service framework is ServiceStack (currently V5.1). On Windows, this is wrapped by the TopShelf library, which provides features that make it easy to install, uninstall, start, stop, and manage a Windows service.

Ace non-GUI plugins are microservice providers. Ace GUI plugins provide the human intefaces to thesse microservices.
ServiceStack is the current microservice provider, and static web server.

Blazor is currently the primary GUI architecture, as it integrate well with both static web servers and with data structure based on .Net components.

Distribution of Ace is done via NuGet packaages and the Chocolatey pacakge management software.

Wherever possible, algorithms and data structures used in Ace are re-factored into utility libraries, to promote code reuse as much as possible.  These utility libraries are managed within the ATAP.Utilities repository. There are currently over 30 packages in this reposity. Some are little more than placeholders with only one or two simple fuctions; other utiltiy libraries contain larger numbers of structures and functions.

Utility libraries are designed so that data structures are packaged in one unit, objects in another, and static functions in a third unit. This allows the data structures to be shared between the GUI code and the microservice code, using serialization mechanisms found in the data structures package.

The process needed to translate the code found in these repositories into versioned distribution pacakges, and integrting these ditribution packages into the exisitign world-wide software distribution system, is not trivial. Three of the ATAP.Utility packages are devoted to the Build Tooling code needed to make this happen. In the course of developing thsse BuildTooling pacakages, a number of issues surfaced, and their olutions implemented. You will find in the documentation library a document devoted to explaining how the BuilTooling parts interact with the building (MSBuild.exe invoked via Visual Studio, and invoked via dotnet.exe), testing/verification (UnitTest, IntegrationTest, End-To-End (E2E) test, Appveyor) and distribution (NuGet and Chocolaty) tool suites.

# ATAP.WebSites.ATAPConsulting
Documentation for the corporate website

## Overview

## Architecture

## Frameworks

## Third-Party Libraries

## Static Assets

### Company Icons

### Images

### Fonts

## Management of Sensitive information used for deployment

## Development

### Development Environments
Development may be done using any appropriate tool, and any appropriate web server host may be used during development.
Initial documentation will be for development using the Visual Studio 2017 IIDE, along with the integrated IIS Express web server host.

### Deployment to Development Web Server Hosts
### 

## Testing

### Testing tools

### Deployment to Testing Web Server Hosts

### Unit Testing

### Integration Testing

## Production

### Deployment to Production Web Server Hosts

# Detailed Instructions for building the ATAPConsulting corporate Web site.

## Development
Instructions for building and testing the web site in development lifecycle stage

### Visual Studio Professional IDE

### Visual Studio Code Community Edition


### Unit Tests
Add NuGet Package reference to xUnit
Add NuGet Package refrence to MOQ

## QA/Testing
Instructions for building and testing the web site in QA/Testing lifecycle stage
### Integration Tests
Add NuGet Package reference to latest Microsoft.AspNetCore.App
Download and install latest .NET Core SDK (2.1 or better) to build and run integration tests
https://www.microsoft.com/net/download

### Automated Continous Integration (CI) tools used

## Production
Instructions for building and testing the web site in its final, production, lifecycle stage

## Deployment
Instructions for deploying the production web site to the hosting provider

## Attributions
https://www.dotnetcurry.com/aspnet/1402/aspnet-core-2-new-features
https://www.dotnetcurry.com/aspnet-core/1414/unit-testing-aspnet-core
https://www.dotnetcurry.com/aspnet-core/1420/integration-testing-aspnet-core
https://docs.microsoft.com/en-us/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-2.1&tabs=aspnetcore2x
https://www.dotnetcurry.com/aspnet-core/1433/end-to-end-testing-aspnet-core
http://www.eidias.com/blog/2016/2/14/automated-ui-testing-in-aspnet-mvc5-using-selenium-webdriver



