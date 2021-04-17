---
Title: Introduction to AceCommander
tags: Ace AceCommander
layout: post
description: The motivation for and introduction to the AceCommander app
category: technical
---


The MySQL a is \called AceCommander, it holds userauth user tables

Install MySql here:

the database files need to be under dropbox, so a my.ini file has to be created, and MySQL has to be told to look for it under a dropbox location.
The current location is under <drive>:/DropBox/MySQLData

every developer, qa, and test environment, as well as every production system, needs its own AceCommander database
the my.ini file specifies this as <drive>:/dropbox/MySQL/data

The MySQL database name, user, and user password is in the configuration file, as part of the MySQL connection string.

Make sure that on the development or QA or production server, that the database exists, and that the specified user has the correct permissions and password set

LiquiBase is the Open Software tool that is used to keep version-controlled information on the MySL database schema and lookup tables' data.

Service stack returns '403 - forbidden' when Blazor GUI makes it's first call to ServiceStack and asks for all of its DLL files. Have to document the addition of .dll to SS allowed file extensions
Service stack returns '403 - forbidden' when Blazor GUI makes it's first call to ServiceStack and asks for all of its PDB files. Have to document the addition of .pdb to SS allowed file extensions. PDB files are for debugging

Also document the V S2019 requirement and the .DotNetCore V3 preview requirement.
Maybe a section on how to upgrade from V0.5.0 to V0.9.0
Document the issue with Blazor.Extensions.logging still being on V.0.7.0, and the conflict it caused, and how Blazor.extensions.Logging had to be ripped out.

Sentinel startup stuff

Document how to add SQLServer to a system, minimal, to use with Ace

For VS 2019:
To automatically close the console when debugging stops, enable Tools->Options->Debugging->Automatically close the console when debugging stops.

So, now enumerations are a code smell? https://github.com/ardalis/SmartEnum and others

Installing Telerik UI components for Blazor: Following instructions, it starts with needing to install nuget.exe; that will make the nuget package push work, as well.
Add to the prerequisites part of the doc the need to download and install nuget.exe, and then to put it on the environment path.

today, that is 32-bit V4.9.4, instal to programfiles(86)/nuget

The follow Telerik instructions on how to add the telerik private feed to visual studio
