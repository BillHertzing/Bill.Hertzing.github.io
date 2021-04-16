---
Title: Client-side Blazor demos
tags: Blazor
layout: post
description: Overview of the BlazorDemos repository
category: technical
---


Until last week, my main app (and my Blazor demos), used ServiceStack middleware hosted in .Net 4.7.1 using the Windows HTTPListener in a Console App. I spent the last week moving the web servers in my demos 06 and 07 to ASP.NET Core Kestrel self-hosted WITHOUT IIS integration. Yesterday and the day before, I got demo06 server working with V3.0P4 SS Middleware in Kestrel WITH IIS intergation, and demo07 working with SS in Kestrel WITHOUT IIS integration. 

Happy to report that one of my demos and my main app have both been upgraded to V3.0 Preview 5. There are (at least one) thing still broken in P5 that were broke in P4;
```
// Issue in Preview 4 & 5  requires the "route" to be a complete URL
var uriBuilder = new UriBuilder("http://localhost:21200/BaseServicesInitialization");
InitializationResponse = await HttpClient.PostJsonAsync<InitializationResponse>(uriBuilder.Uri.ToString(),initializationRequest);
```
But that will make me take the time to figure out how to configure both the host and the port at runtime instead of being lazy and hardcoding them as I've done so far...
Lots more testing to go do, now...

 here's a gist with my program.cs file, and how I eventually got it to work in P5
 https://gist.github.com/BillHertzing/d0a27b2dcdf29ffce1b3f9d1e5413497
 Thats the first public gist I've shared, please let me know if you have issues seeing it.
 
 LaunchSettings.json : only applicable to a ASP.NET Core console host (or service) running a web server
 : should not be under any GUI projects
 : should be under all Server projects
 : should define profiles for the Development, Testing,Staging, Production environments. Testing is a custom environments
 

 The "applicationUrl": "http://localhost:21250/" found in LaunchSettings.json must match the current "ListenOn" that the web server is running, or else it will not launch a browser. In a launchsettings.json Profile, it associates a project's executable environment with an endpoint the application hosted in the web server will respond on. Together they provide a channel that the developer can use. Visual Studio uses it to determine if it will launch a browser. 
 





Top level ReadMe

## Demo01

Starting with the basics. Introducing the development environment / the development tools. The most basic of the Demos: a GUI and a WebServer; Introducing the Blazor GUI running in/on WASM in the browsers. Introducing the `index.razor` page. Introducing logging in the GUI via Microsoft.Extensions.Logging and the Blazor.Logging.Extensions. Introducing the WebServer; in Demo01, a Framework 4.7 ConsoleApp running a default WebHost over HTTP.Sys. Introducing the ServiceStack Middleware host, using ServiceStack logging and NLog. Introducing Sentinel, a UDP log capture and viewing rool. Explanation of how the WebServer servers the static files that make up the Blazor GUI. Introduction to the basic debugging tools for the GUI and for the WebServer.

## Demo02
### The GUI focuses on Blazor basics, 
* The GUI adds a CodeBehind page `index.razor.cs` for the `index.razor` page. 
* The GUI adds `AnIntegerProperty` to the CodeBehind page and adds its visual display to the `index.razor` page. 
* The GUI adds to `index.razor` and `index.razor.cs` the visual representation and the c# code to support a button called `IncrementAnIntegerPropertyButton`. 
* The GUI adds an implementation of a simple `OnClick` handler which increments the value of the `AnIntegerProperty`.
* Discussions on the transient nature of data in the browser.
* Styling focuses on the site.css file
  * The site.css file adds a background color for the body of the `index` page.

### The Server focuses on the IntegratedIISInProcess WebHost
* References to .Net Core V2.1 are added to the .csproj
* The Server adds ....
* Discussions on how the WebServer serves the static files that make up the Blazor GUI.
* launchsettings.json is introduced, and contains settings for running /debugging the  IntegratedIISInProcess WebHost.
* The ServiceStack middleware is hosted in the IntegratedIISInProcess WebHost.

### The build / debug tooling 
* Discussion on how the Server is started, both with and without debugging, from Visual Studio and from the CLI. 

### details for the Demo02 readme
The Server moves the SSApp middleware into an IntegratedIISInProcess WebHost running under .Net Core V2.1.
A static method for the creation of an IWebHostBuilder configured to create an IntegratedIISInProcess WebHost is introduced.
Within the static method, the extension method WebHost.CreateDefaultBuilder() is used to return an IWebHost pre-configured with the defaults necessary to run as an IntegratedIISInProcess WebHost.
launchSettings.json refers to IISExpress
The GUI 's one page gets a local variable and a button to increment it. Discussions of persistence of data in a browser-hosted GUI. The site.css file is modified to produce a background effect. The Server appears, a .Net Core 2.1 WebHost running all the defaults (IntegratedIISInProcess). This replaces the ConsoleApp of Demo01.  launchsettings.json is introduced, and contains settings for running the  IntegratedIISInProcess WebHost. The Blazor GUI project introduces a button, and the button's OnClick handler


## Demo03 - GUI gets browser-local storage, Server moves to .Net Core V2.2 and Kestrel WebHost
### The GUI focuses on browser-local storage
* The GUI adds the third-party Blazor library [Blazored.LocalStorage]().
* The GUI uses the synchronous interface to `Blazored.Localstorage` persist the value of the page-local `AnIntegerProperty` via that property's getter and setter.
* Styling focuses on the `site.sccs` file
  * The `site.css` file is migrated to the `site.sccs` file.
  * The background color of  the Body tag is modified.

### The Server focuses on the Kestrel WebHost
* References to .Net Core V2.2 are added to the .csproj
* The Server adds a static method for the creation of an `IWebHostBuilder`.
* launchsettings.json adds a section to support launching the Kestrel-based Server.
* The ServiceStack middleware is hosted in the Kestrel WebHost.

### The build / debug tooling focuses on adding support for .sccs files
* The Visual Studio build tooling adds the VSIX extension [Web Compiler](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebCompiler). Visual Studio is configured to compile any `.sccs` file into a `.css` file and a `.min.css` file, both of which are copied to the GUI's ContentRoot folder during build / publish..

### details for the Demo03 readme
A site.sccs file, and tools to compile the site.sccs file to the site.css file, are introduced.
The server project targets Net Core V2.2. A KestrelAlone WebHost is introduced.
The site-wide site.sccs file is added to the wwwroot/css directory. The contents of the current site.css is copied into the new site.scss file for the GUI.
The GUI references the third-party Blazor library Blazored.LocalStorage.
The synchronous interface to Blazored.Localstorage is used to persist the page-local `AnIntegerProperty` via that property's getter and setter.
The server moves the SSApp middleware into a KestreAlone WebHost running under .Net Core V2.2.
A static method for the creation of an IWebHostBuilder configured to create a KestreAlone WebHost is introduced.
Within the static method,  a new WebHost is configured with no defaults by new()ing an instance of the WebHostBuilder class then applying the extension method .AddKestrel() and others.
 launchsettings.json are expanded to include settings for KestrelOnly
The GUI's local variable takes on persistence in browser-local storage using [Blazored.LocalStorage]() by [Chris Sainty]().  Mads Kristensen  Web Compiler is installed to Visual Studio, the wwwroot/site.css is migrated to site.scss, and the build tools extended to process .scss files. The Server targets .Net Core 2.2. The WebHost in this Demo is Kestrel (alone).  launchsettings.json are expanded to include settings for KestrelOnly

## Demo04 - GUI adds visual attributes and async event handlers,  Server get Environment Variables and a selectable WebHost
### The GUI focuses on 
* The GUI gets some big changes. `AnIntegerProperty` is placed within a text span `AnIntegerPropertyTextSpan` for styling with the `AnIntegerPropertyTextSpanStyle` page-local property. The `IncrementAnIntegerPropertyButton` adds three page-local properties for `class`, `style`, and `text`. The button's `OnClick` event handler binding becomes async and indirect. The GUI now has two possible `OnClick` event handler methods, one for `Active` an one for `LogThenIgnore`, with 'Active' being the initial handler for the button. 
* Clicking the button, when Active, adds visual modifications to the button and to the `AnIntegerPropertyTextSpanStyle`, changes the event handler to `LogThenIgnore`, increments the value of `AnIntegerProperty` via a simulated async operation with a 4 second delay before returning, and then again changes the visual attributes and the event handler of the button back to 'Active'.
* Discussions on how async event handlers interact with async Tasks and TaskContinuations.
* Styling focuses on variables in the `site.sccs` file.
  * The .sccs file adds ....

### The Server focuses on Environment Variables, remains on .Net Core V2.2
* The Server adds the ability to allow the developer to select either of the two web server hosts, KestrelAlone or IISIntegratedInProcess, to be used when starting the project's executable. 
* Discussions on Environment variables
* `launchsettings.json` adds Environment Variables, and uses `BlazorDemos_WebHostBuilder` to select which WebHost to build.
* The ServiceStack middleware adds ....

### The build / debug tooling ... 
* Examples of selecting the WebHost for debugging sessions started from either Visual Studio or the CLI are discussed.

### details for the Demo04 readme
Discussions on async event handlers in the context of the UI thread. Making all of the StateChangeEventHandlers into async Action<task> signatures makes it possible to store them en-group in the State object. They can be lambdas, or they can refer to methods belonging to the CodeBehind classes / file. They can be retrieved from the IEnumerable<Func<Task>> collection with a LINQ query.  Launchsettings.json are introduced to allow the developer to select either of the two static WebHostBuilders when starting a debugging session.
New in this Demonstration are 
1. a second entry in the launchSettings.json Profiles list
1. environment variables introduced into the individual entries of the launchSettings.json Profiles list
1. How to read environment variables before the web host is created so that the program can decide what kind of a web host to create

## Demo05 - GUI gets a Timer, and State, Server gets .Net Core V3.0, Environment and environment-aware features.
### The GUI focuses on 
* Discussions on various GUI State approaches 
* The GUI adds a State class to reduce the repetitive boilerplate needed for c# property representation of visual and action attributes of the HTML page / elements.
* The GUI adds a new DI-injected State object and its methods is used to store the Action<Task> methods for the statechange handlers, along with a LINQ-based query to retrieve the correct `MethodToUse`.
* The GUI adds a timer, an animated gif file to represent the timer, and two event handlers for the timer, `Expired` and `LogThenIgnore`. 
* The GUI Timer Expired statetransition handler does nothing to any properties bound to `AnIntegerProperty` and `AnIntegerPropertyTextSpanStyle`. The  Expired state program does change the style of the timer gif for a timed delay of 0.5 seconds using `Task.Delay(500)` then changes it back and resets and restarts the timer.
* The GUI starts using string constants for the class, style, and text properties for the `AnIntegerPropertyTextSpanStyle` and for the `IncrementAnIntegerPropertyButton` button's visual attributes (for both Active and queuing visual effects). 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on .Net Core V3.0., the GenericHost, and environment
* Discussion on the .Net Core V3.0 GenericHost and hosting a WebHost within the GenericcHost
* References to .Net Core V3.0 are added to the .csproj
* Discussion on the concept of Environment (Production, Staging, Debug, etc) and the use of the `ASPNETCORE_ENVIRONMENT` environment variable. Discussion on localization of this environment variable, and how to select which WebHost to build/run/use based on the value of this environment variable.
* The Server adds error pages based on environment, along with 'Development-environment-only' features.
* `launchsettings.json` grows to support four runtime choices consisting of two Environment choices and two WebHost choices.
* The ServiceStack middleware adds ....

### The build / debug tooling adds 

### details for the Demo05 readme 
* Note that having both a button OnClick Active event handler and the TimerExpired Active event handler both "active", means that the program is multiplexing those two statechange inputs. The program  can be in the midst of responding to one, when the other occurs, which can lead to synchronicity issues. In Demo05, the program is written so that there is no interaction between the two active statechange handlers, hence no need (yet) to synchronize access to state variables from the two statechange handlers. Also note that having an animated gif in the visual display can provide a clue if the main browser UI thread is blocked.


## Demo06 - GUI Timer enhancements, Enumerations, SupportedWebHosts, and either Kestral and IntegratedIISInProcess in the Server 
### The GUI focuses on 
* The GUI adds a button to start/stop the timer, a CSS animation to represent the timer enabled boolean, and event handlers for the button
* State 
* Styling focuses on CSS Animations and .sccs include files
  * The `site.sccs` file adds styles for the TimerControl button, 
  * The GUI project adds a new .`.sccs` file fragment suitable for including into the `site.sccs` file.
  * The new `.sccs. file fragment contains a CSS Animation
  * animations is triggered visible-running / invisible-disabled by the expiration of the Timer trigger.
  * Further styling via String.Constants to make the elements visually explanatory as the demo is run through its visual states.

### The Server focuses on a single static builder for the GenericHost, which incorporates different webHostBuilder configurations based on a parameter to the method. The multiple static builders are removed.
* References to .... are added to the .csproj
* The Server adds an enumeration for `SupportedWebHostBuilders` and validates/parses the `BlazorDemos_WebHostBuilder` environment variable against this enumeration.
* The Server merges the two static `IWebHostBuilders` into a single parameterized static builder method `CreateSpecificHostBuilder(SupportedWebHostBuilders webHostBuilderToBuild)`.
* A new compilation unit is introduced `Enumerations.cs`. The class `Program` in `Program.cs` is made into a `partial` class, and the new Enumerations.cs also contains a declaration of `partial Program`
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling

# Cut Line for version 1.5.0 
### Demos below this line are still under active development in the various features Branches and the develop branch, and in the last few cases the demo is still completely TBD.

## Demo07 - Configuration (Part1)
### The GUI focuses on Configuration (TBD when CSB supports Extensions.Configuration)
* The GUI adds a new compilation unit `DefaultConfiguration.cs`, which contains the minimal configKeys needed to run the GUI in production 
* A discussion on concurrency if two or more event handlers try to access the same state variable(s)
* State element properties for data and visual attributes get their setters hooked to NotifyPropertyChange-like and NotifyPropertyChanging-like events 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on creating a `configurationRoot` and the `Microsoft.Extensions.Configuration` class
* Discussions on the concept of Configuration (ConfigurationBuilder, Configuration Providers, and a ConfigurationRoot) is introduce
* References to `Microsoft.Extensions.Configuration` are added to the .csproj
* The Server adds a new compilation unit `DefaultConfiguration.cs`, which contains the minimal configKeys needed to run the program in production For Demo07 and future, that minimum includes at least the list of URL(s) to ListenTo.
* The Server adds an initial hostConfigurationRoot created from InMemory, File, and EnvironmentVariable providers.
* WebHostToBuild and Environment strings from the ConfigurationRoot are validated. If not present, defaults are provided and added to the ConfigurationRoot.
* `launchsettings.json` adds environment variable for the list of URLs that the Server is expected to ListenOn.

* The ServiceStack middleware adds ....

### The build / debug tooling ...

### details for the Demo07 readme 
The static `IHostBuilder` method `CreateGenericHostBuilder()` grows an additional parameter of type `ConfigurationRoot`, and the `hostConfigurationRoot` is passed to the method
The Environment value retrieved from the hostConfigurationRoot is used to conditionally apply the Development-only configuration options.
The Development-only configuration options are moved into the static `CreateGenericHostBuilder()` method.


## Demo08 - Async Tasks and WaitAny in the GUI, Configuration (Part2) in the Server
### The GUI focuses on visual representation of a simple async task's 
* lifecycle: initialization, quiescent, dispatch, awaiting, synchronization, task continuation, completion . 
* The GUI adds an async method that returns a Task, a button that dispatches it, and  visual badge for the task's status and results. 
* Notation and relationships of state triggers, as exemplified by buttons, timers, and tasks, are abstracted as a Linq query.  
* The browser-local storage properties involved with State get a concurrency flag. 
* Additional expansion of Configuration if warrented after Blazor supports it.

### The Server project focuses on adding *Detailed environment-specific configuration settings*
* the `Microsoft.Extensions.Configuration` to including the concept of `Environment` (Production, Development, Testing, etc.) driving the contents of the ConfigurationRoot
* The static `IHostBuilder` method `CreateSpecificGenericHostBuilder()` adds AppConfiguration based on a chain of Configuration providers.
* The AppConfiguration includes 
  1. CommandLine Arguments
  1. Environment variables, filtered by a prefix
  1. How to branch the flow of execution based on `Environment`, and how to name the settings files.
  1. Settings file(s) in JSON format, Production, and additional settings based on Environment, for both the GenericHost and the WebHost
  1. compiled-in defaults for the `Environment`

* `launchsettings.json` ...
* The ServiceStack middleware adds ....

### The build / debug tooling ...


## Demo09 - Logging in the Server and synchronicity in the GUI
### The GUI focuses on logging (TBD when CSB supports Extensions.Logging beyond just the Console Logger)
* Discussions on how to accomplish Logging from a browser, that is browser-independent and platform-independent.
* (TBD) The GUI adds Serilog as a logging provider for the CSB GUI application, which writes to the DebugConsole sink, whihc, when run under IISINtegrated, will write-back to the Visual Studio Debug output console
* The statechange methods for the Timer and for the asynch task are modified so they also increment the IntegerProperty.
* Styling focuses on 
  * The .sccs file adds 

### The Server focuses on Microsoft.Extensions.Logging using Serilog as the logging extension
* References to Serilog are added, and references to NLog and ServiceStack logging are removed.
* Log statements that used string expansion are replaced with SeriLog structured logging
* Discussions on how to add / reference SeriLog as a MEL logger, how to configure logging in a ConfigurationRoot, and how to view logging in a stream database (SEQ).
* launchsettings.json ....
* The ServiceStack middleware adds ....

### The build / debug tooling adds SEQ for log collection and viewing ,along with a discussion on how to use it with these Demos.
An external tool `Seq` is added to provide centralized log collection and viewing. Log messages are ingested as HTTP messages to `localhost` on the default port 5341
______________
## Server
This demo focuses on Logging
The `ServiceStack.Logging` dependency and using is removed from all compilation units (source .cs files)
The `Microsoft.Extensions.Logging` NuGet Package dependency is added to the project
Serilog dependencies (NuGet Packages) are added to the project: (`Serilog, Serilog.AspNetCore, Serilog.Enrichers.Thread,S erilog.Exceptions, Serilog.Settings.Configuration, Serilog.Sinks.Console, Serilog.Sinks.Debug, Serilog.Sinks.File, Serilog.Sinks.Seq, SerilogAnalyzer`)
The `genericHostSettings.json` and `genericHostSettings.development.json` files grow an extensive logging sections for `Microsoft.Extensions.Logging` and for Serilog
`genericHostSettings.json` (production) configures Serilog with the `Seq` writer. The Serilog `LogContext` is enriched with the current threadID, and an additional property, `Application` having the value 'Demo09"
`genericHostSettings.json` (Development) configures Serilog with the `Seq` writer, the `Console` writer, and the `DebugOutput` writer. 
The Serilog static Log object is initialized with the Serilog configuration read from the ConfigurationRoot
The static method CreateGenericHost adds `Serilog.AspNetCore` logging to the genericHost's `ConfigureWebHostDefaults` builder extension and to the `.ConfigureLogging` builder extension via `.UseSerilog()`
The NLog.config and NLog.xsd files are removed. 
The Serilog Analyzer, installed via NuGet, will provide IntelliSense for the Serilog Log methods.
logging statements throughout the code are replaced with SeriLog structured  logging statements 
The Log statements that used String expansion are replaced with SeriLog structured logging messages. The Analyzer provides a suggested replacement, so this step is just a "replace all occurrences" in the project
________

## Demo10 - Server: Tracing and Profiling via Event Tracing for Windows (ETW), GUI: simple Task
This is the specific documentation for Demo10, *Adding Event Tracing for Windows (ETW)*.
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 
### The Server focuses onTracing and Profiling via Event Tracing for Windows (ETW)
* The server adds the ability to log method boundaries in the ETW tracing window (not getters or setters yet) 
  * A managed ETW provider, named `DemoETWProvider`, derived from `EventSource` is added.
  * The `DemoETWProvider` class has one static Property, `Log`, which holds an instance of the `DemoETWProvider` class.
  * The `DemoETWProvider` has one method, `Information`, which writes to the ETW subsystem via `System.Diagnostics.Tracing`.
  * The Serilog logging messages for method entry and exit throughout the Server classes are replaced with calls to the `DemoETWProvider.Log.Information`
* A number of external tools useful for collecting, viewing, and analyzing ETW events are discussed in the documentation, along with links to further information
  1. Visual Studio Diagnostics Event window
  1. PerfView, and how to use it to collect ETW events from the demo, and view the ETW logs
  1. ToDo: --WPA, Windows Performance Analyzer--
 

## Demo11 - ILWeaving using Fody 
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on adding Fody for ILWeaving, and the MethodAspectBoundry weaver AddIn for Fody
* Discussions on what ILWeaving is, and using Fody to accomplish it
* Discussions on  
* References to MethodAspectBoundry.Fody are added to the .csproj
* A new Attribute `ETWLogAttribute` is defined, added to almost every class, and all method entry and exit logging statements are removed. 
* The Server uses the MethodAspectBoundry Weaver to add ETW logging for every method in a class
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling adds ILWeaving package

## Introduction
The Blazor GUI project ...
Todo: The server project focuses on the details of ILWeaving using Fody to provide ETW logging of method entry and exit, including getters and setters. MethodBoundryAspect Fody Plugin also logs exceptions to ETW automagically.
ToDo: look some of that, and move to the next demo.The server project focuses on the details of installing the server project as a Windows service, and partially automating that process.
The Common DTOs ..



## Demo12 - Publishing both the  GUI and the Server into a Windows Service
### The GUI focuses on getting the new `PublishedService.pubxml` file setup properly.
* The GUI adds the ability to publish to a specific folder within the _\_PublishedAgent\PublishedService_ subdirectory tree using the `PublishedService.pubxml` publishing option 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on creating the basic windows service additions, then hosting the ServiceStack middleware in a Kestrel-only webHost inside a GenericHost under Net Core V3.0 and running it as a Service
* References to .... are added to the .csproj
* Discussion on the differences between a ConsoleApp and a Service
* Discussion on concepts from the Runtime, to determine if the program is running under Windows or Linux
* The Server adds a key runtime variable  `IsConsoleApp` to determine if the program is running under Windows or Linux
* The Server adds switchMappings ConfigurationRoot to detect -C or -Console as a command-line switch
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling focuses on the Windows sc.exe utility
* Discussion on using `sc.exe` for manually installing and uninstalling the genericHost as a Windows Service are documented 
* Discussion on how to setup VisualStudio and the CLI to 'Publish' the Server to a specified location, which can be referenced by `sc.exe`

### Publishing Steps
* Demo12 adds a new section to the ReadMe for documenting what changes get made in the publishing process. 
* The initial section describes the manual steps for creating / publishings, installing, and running the server as a service, how to uninstall it, and the run edit compile cycle for developing the service..

## Demo 13 - (TBD) Automating Publishing
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The build / debug tooling focuses on 
a discussion of the InstallUti;l

You will need to install a `.Net Core Global Tool` called `installUtil`. From a VS 2019 command prompt, run `dotnet tool install -g --framework netcoreapp3.0 --version 1.2.0 InstallUtil`. Of course check that this is still the latest version and adjust the instructions accordingly, if a later version exists.

### Publishing Steps
* focuses on automating the publishing process, and provides a PowerShell script `PublishingAutomation.ps1`


## Demo14 - (TBD) Publishing both the GUI and the Server to Windows Subsystem for Linux as a Daemon
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on 
* References to .... are added to the .csproj
* The Server adds ....
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling ...

## Publishing Steps


## Demo15 - (TBD) Publishing both the GUI and the Server to Linux kernals
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on 
* References to .... are added to the .csproj
* The Server adds ....
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling ...

## Publishing Steps

## Demo16 - GUI and Server open communications
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on 
* References to .... are added to the .csproj
* The Server adds ....
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling ...

## Publishing Steps

## Demo17 - GUI and Server PlugIns
### The GUI focuses on an implementation of additional pages defined in Configuration and loaded at runtime
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on an implementation of additional services via the SS Plugin structures
* References to .... are added to the .csproj
* The Server adds ....
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling ...

## Publishing Steps


---- Cut Line ----
Rough notes below, to be integrated

ToDo: InstallUtil? Registering messages with Windows Application EventLog?
Details in [Demo12 Server](Server/ReadMe.html)

Demo13 - The GUI focuses on .... The GUI adds .... Discussions on .... The .sccs file adds .... The build tooling adds... The Server focuses on .... References to .... are added.... Discussions on .... launchsettings.json .... The ServiceStack middleware adds .... The CommonDTOs adds ...


The AppConfiguration includes 
  1. CommandLine Arguments
  1. Environment variables, filtered by a prefix
  1. How to branch the flow of execution based on `Environment`, and how to name the settings files.
  1. Settings file(s) in JSON format, Production, and additional settings based on Environment, for both the GenericHost and the WebHost
  1. compiled-in defaults for the `Environment`
The AppConfiguration includes
AppConfiguration 
CommandLine Arguments
Environment variables, filtered by a prefix
Settings file(s) in JSON format, Production, and additional settings based on Environment, for both the GenericHost and the WebHost
compiled-in defaults for the Environment
event handlers
How to branch the flow of execution based on Environment, and how to name the settings files.
logging statements
ETW provider, named `DemoETWProvider`, derived form `EventSource`
System.Diagnostics.Tracing
The Serilog logging messages for method entry and exit throughout the Server classes are replaced with calls to the `DemoETWProvider.Log.Information`
  1. Visual Studio Diagnostics Event window
  1. PerfView, and how to use it to collect ETW events from the demo, and view the ETW logs
ETWLogAttribute
[ETWLogAttribute]
logging messages for method entry and exit throughout the Server classes are
Blazored.LocalStorage



 
 The Blazor GUI site.scss file uses variables to define the <body> tags background style / color.

Blazor.Logging.Extensions

Logging  in the GUI via Microsoft.Extensions.Logging, and Blazor.Logging.Extensions

Blazored.LocalStorage

Blazored.LocalStorage

The Server adds Environment variables, and uses one to select which WebHost to build/run/use.  launchsettings.json grows Environment variables.
Environment Variables and LaunchSettings.json grow to add Environment
.Net Core 2.2
The .sccs file adds styles for AnIntegerProperty, and IncrementAnIntegerPropertyButton (for both Active and queuing visual effects)
The GUI adds a timer that will increment AnIntegerProperty, a button to start/stop the timer, styles for the TimerControl button, and state triggers for the button and for the timer itself
The .sccs file adds styles for AnIntegerProperty, and IncrementAnIntegerPropertyButton (for both Active and queuing visual effects).
The GUI adds a timer that will increment AnIntegerProperty, a button to start/stop the timer, styles for the TimerControl button, and state triggers and state transitions for the button and for the timer itself.
The Server adds Environment variables, and uses one to select which WebHost to build/run/use.  launchsettings.json grows Environment variables. The Server targets  .Net Core 3.0 and will remain so for the rest of the demos (Currently Preview6)
The GUI adds a timer that will increment AnIntegerProperty, a button to start/stop the timer, styles for the TimerControl button, and state triggers and state transitions for the button and for the timer itself.  
Demo06  -  The GUI adds a second integer property `AnotherIntegerProperty`, a  button to increment it, and a fourth button that will increment both `IntegerProperties`.   Further styling to make the elements visually explanatory as the demo is run through its visual states. Our browser-local storage properties involved with State get their setters hooked. A discussion on concurrency if two or more substates try to access the same state variable
 The Server adds the concept of Environment (Production, Staging, Debug, etc). Discussion on localization of these values, and uses one to select which WebHost to build/run/use.  Environment Variables and launchSettings.json grow to add Environment.
Demo06  -  The GUI adds a second integer property `AnotherIntegerProperty`, a  button to increment it, and a fourth button that will increment both `IntegerProperties`.   Further styling to make the elements visually explanatory as the demo is run through its visual states. Our browser-local storage properties involved with State get their setters hooked. A discussion on concurrency if two or more substates try to access the same state variable.   The Server adds the concept of Environment (Production, Staging, Debug, etc). Discussion on localization of these values, and uses one to select which WebHost to build/run/use.  Environment Variables and launchSettings.json grow to add Environment. 
focuses on a single static builder for the GenericHost, which incorporates different webHostBuilder configurations based on a parameter to the method. The multiple static builders are removed.
A new enumeration `SupportedWebHostBuilders`is introduced,
Demo07  -  The GUI adds an async method that returns a Task, a button that dispatches it, and  visual badge for the task's status and results. Notation and relationships of state triggers, as exemplified by buttons, timers, and tasks, are abstracted as a Linq query.     Our browser-local storage properties involved with State get a concurrency flag. A discussion on concurrency if two or more substates try to access the same state variable.   The Server focuses on a single static builder for the 3.0 GenericHost, which incorporates different WebHostBuilder configurations based on a parameter to the method. The multiple static builders are removed. A new enumeration SupportedWebHostBuildersis introduced, and corresponding environment variable and launchsettings.json entries
Demo07  -  The GUI adds an 
Demo07  -  The GUI adds
The AppConfiguration includes 
  1. CommandLine Arguments
  1. Environment variables, filtered by a prefix
  1. How to branch the flow of execution based on `Environment`, and how to name the settings files.
  1. Settings file(s) in JSON format, Production, and additional settings based on Environment, for both the GenericHost and the WebHost
  1. compiled-in defaults for the `Environment`
The AppConfiguration includes
AppConfiguration 
CommandLine Arguments
Environment variables, filtered by a prefix
How to branch the flow of execution based on Environment, and how to name the settings files.
Settings file(s) in JSON format, Production, and additional settings based on Environment, for both the GenericHost and the WebHost
compiled-in defaults for the Environment
event handlers
How to branch the flow of execution based on Environment, and how to name the settings files.
This demo focuses on Logging
Server adds Microsoft.Extensions.Configuration
genericHostSettings.json
`genericHostSettings.json` and `genericHostSettings.development.json` files grow an extensive logging section
logging statements
ETW provider, named `DemoETWProvider`, derived form `EventSource`
System.Diagnostics.Tracing
The Serilog logging messages for method entry and exit throughout the Server classes are replaced with calls to the `DemoETWProvider.Log.Information`
  1. Visual Studio Diagnostics Event window
  1. PerfView, and how to use it to collect ETW events from the demo, and view the ETW logs
ETWLogAttribute
[ETWLogAttribute]
logging messages for method entry and exit throughout the Server classes are
Blazored.LocalStorage

TEMPLATE:

## DemoXX - XXX 
### The GUI focuses on 
* The GUI adds 
* Discussions on how to 
* Styling focuses on 
  * The `site.sccs` file adds 

### The Server focuses on 
* References to .... are added to the .csproj
* The Server adds ....
* Discussions on how to ....
* `launchsettings.json` ....
* The ServiceStack middleware adds ....

### The build / debug tooling ...



------

