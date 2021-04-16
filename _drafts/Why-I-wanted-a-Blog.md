---
Title: Case for a non-anonymous Internet, Part 01
tags: "Non-Anonymous Internet"
layout: post
description: Justification to not allow anonymous comments on my site and posts.
category: political
---

## TL DR

Making people use their true identity when posting comments to my blog posts might make them more civil. It also allows for the creation of a history of behavior.

## Introduction

ToDo: add content

## Studies showing the incident and degree of hateful speech declines when true identity is required

ToDo: add content

## Studies showing the incident and degree of hateful speech increases when anonymity is allowed

ToDo: add content

## Conclusion

ToDo: add content

## Implementation

ToDo: add content

## Attributions

ToDo: add content



Introduction

## Introducing BillHertzing blogs (the technical ones)

I'm here to show that a single individual, retired from a career in computer engineering, can  put together a satisfying experience for contributing to forwarding the state of the art in software engineering. This means doing it as much as possible in free, open source software (OSS). But not completly free, as I've chosen to spend a bit of my retirement money on upgraded components. I spend maybe $1,000 USD a year in software licensing fees, which is not cheap but covers about 6 paid licenses for various tools. There are plenty other tools I would like to have / use, but I no longer have the luxury of a corporate backer to purchase tools for my use. And free tools usually are limited in what they can do, compared to the paid ones. Not saying free ones can't do it all, but you usually have to string together multiple free tools, and that takes more time...

The biggest names in cloud osting are teh biggest software copanies; Microsoft, Google, Amazon. But each tries hard to lockk you into their ecosystem,. I wanted a hosting company that was not so mono-focused, so I chose 1And1 IONOS 

Since you are reading this on my blog, let me tell you how I got blogging, and my web sites,  to work. I think, at a minimum, you need a web host that can run the WordPress web server, and the backing database. Of course you need your public GitHub account and repositories (or other SW hosting for OSS software with public access). You will need to host the "programs you are developing", with Internet facing access, and probably with some kind of database persistence. Finding the solution that combines the most capabilities, the fewest places that have to be 'touched'

I'm hosting this blog on a WordPress installation I downloaded and installed to a 1And1 Windows WebHosting Plan (actually not working yet, this blog is not yet published). I don't haave to pay for WordPress, its free, but the Web Hosting costs me about $13 / month. That includes SQLServer databases and MySql databases, one or more I can activate and integrate with WordPress.

The 1And1 plan also provides an IIS webserver, and space for files. I can put up two domains public facing to the Internet, and as many subdomains of those that could possibly be needed. The fee I pay 1And! includes the ICAN registration abd DNS administration for those domains. I can use my favorite free FTP client, WinSCP,  to connect to the 1And1 webspace the IIS server 'sees'.

I use Microsoft's Visual Studio  Professional Edition (and pay for it), because I find having the integrated Test runner helps boost my productivity and code quality. I pay for CodeRush from DevExpress to help boost my productivity while inside VS, as it will complete many boilerplate tasks. The dotnet CLI tools, are free, and the both the CLI tools and VS can 'Publish' to the 1And1 Webspace files.

I am writing a program that will help you make / string together programs that automate some of your ToDos in real life. The program I'm writing runs anywhere .Net Core 3.0 runs, uses a Blazor interface, supports a bare minimum "I'm here" in minimal mode, but can be expanded by the enabling of features and loading of PlugIns. PlugIns are designed to share their public data, methods and events with each other.

I'm also publishing a series of Demo programs that explain in detail the concepts and constructs used in the AceCommander program. This is ensure I understand, and can explain, what 'the code I got from goggling the Internet' is doing when I use it. The Demos are also another way I want to give back and help others understand how the C# language and the .Net  libraries can be used.

I'm publishing my work now because it has reached a stage I need to invite comment and criticism, and to  do that I have to announce it exists, and have a place where people can stop by and have a look. The whole thing is certainly still in early stages, but I invite you to come along for the ride in the coming months.

