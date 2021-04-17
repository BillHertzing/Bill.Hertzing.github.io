---
Title: Why I wanted a Blog
date: 2021-04-17 12:00:50 -0600
tags: 
layout: post
description: The motives that led me to start this site
category: political
---

## TL DR

- As a place to share knowledge, tips and how-tos, mostly regarding development, operations and monitoring of computer systems.
- As a place to publish the reasoning that underlie my personal stance on sometimes controversial political issues.
- As a place to share pictures and stories about myself and my family to other family members and our friends.

## Introduction

I have always envied the developers who do a good job communicating with the world. They enjoy a connectivity to others that seems it must enrich their lives. I've always wanted my own blog site where I can write about whatever interests me, technically, politically, and personally. I have had three previous forays into blogging. Once using Blogger at Google, once trying to host my own site at 1And1 (now IONOS), and once with a site at wordpress.com. In each of these prior attempts, I've foundered on the technical implementation. Either the platform didn't have the features I wanted, or the learning curve was too steep, or the cost was prohibitive. Now I'm about to try launching my fourth attempt, using the static site generator Jekyll, with the pages served by GitHub. Here's hoping that this time I'll be long-term successful!

## About the `ATAP` name used in the app and library branding

The last 12 years of my career I owned and operated a *microISV*, a company with a very small number of employees that focused on providing consulting services. The name of the company was ATAP Technology, Inc. All the code I wrote on my own during that time, (the portion of code which was not directly funded by my customers), used the namespace and branding of ATAP Technology. When I retired, I closed the company. That body of code I have continued to use and extend in my Open Source Software projects. As the author of the code, and the prior owner and CEO of ATAP Technology, I have placed it into the public domain under the MIT license. I'd love to hear from any lawyers on how best to ensure the code I've written and published stays in the public domain.

## Technical postings

I'm here to show that a single individual, retired from a career in computer engineering, can put together a satisfying experience for contributing to the state of the art in software engineering. This means doing it as much as possible in free, open source software (OSS). But not completely free, as I've chosen to spend a bit of my retirement money on upgraded components. I spend maybe $500 USD a year in software licensing fees, which is not cheap but covers paid licenses for various tools. There are plenty other tools I would like to have / use, but I no longer have the luxury of a corporate employer to purchase them! Free tools usually are limited in what they can do, compared to the paid ones. Not saying free ones can't get the job done, but you often have to string together multiple free tools, and that takes more time. The technical posts here will offer insights into how to use various free tools and how to combine them to make development and writing about development easier.

The technical posts fall into two broad categories. The first category are posts that discuss the OSS application and libraries that I am creating. The second category deals with tips and how-to posts regarding specific tools, libraries, and techniques I use in my day-to-day development activities.

I'm publishing my work now because it has reached a stage I need to invite comment and criticism, and to do that I have to announce it exists, and have a place where people can stop by and have a look. The other obvious (to me!) reason is that there is probably only about a decade of my life left to try and give back to the OSS community a meaningful contribution, and if I don't start now, then, as Pink Floyd said "... no one told you when to run, you missed the starting gun...". The whole application, library, and blog site pastiche is certainly still in it's early stages, but I invite you to come along for the ride.

### The OSS app and libraries that I write

I have often espoused to my friends my dreams of building a wide-ranging multi-function application. That application resides in the repository named `Ace`. As much as possible, the code base for `Ace` is factored into multiple Nuget packages bundled under the `ATAP.Utilities` repository. There are additional repositories that expand on, test, and document specific packages found under the `ATAP.Utilities` repository. I use these as communication and teaching tools to provide deeper insights into the details of the packages, and to interact with other developers to extend and enhance the packages functionality.

The relationships between the repositories I've created is explained in the post *[Repository Inter-Relationships](https://ToDo:). Still in Draft*

## Political postings

All too often, friends and acquaintances repost stuff on social media with no critical thinking. It is easy to hit `share` when something that resonates as 'true' or funny appears, without spending hardly any time to think about it and decide if it true or not, or if it causes anger to a faction of people. When a social issue that is a hot button with my friends appears, my preference is to dig into news and opinions, think about it, and sometimes take the time to write down my conclusions and reasoning. In the past, I've posted long comments on friends' Facebook pages, *(haha, you know who you are)*. I'd rather post those screeds here for general access, instead of on a single social media platform.  I'm hoping to figure out a way to reach my friends and acquaintances through their preferred platform, and notify them when I write a *political* post here, in order to ask them for their opinions and feedback.

## Pictures and Stories

Such fun it is, to work on a mashup of text, images, and video of your latest family event for hours, so you can share it with world. Then you post it to your preferred platform, only to learn that many of your friends didn't see it. Why? Because "oh, I don't spend much time online on blah anymore, I'm mostly online on bleh.". Frustrating, isn't it? So I'll try doing that same mashup of text and images memorializing our next fun outing or family get-together on this blog site, using the Jekyll toolchain to stich it all together, and a cloud service like Dropbox to host the media, and a CDN like Cloudflare to make access quicker. Some posts and media I'll make available to the world, and others will be only accessible if granted access. Then all I need is a notification to friends and family to "take a look". For that, I can educate them on RSS Feeds, IFTTT, how to subscribe to the Bill's Blog RSS feed, and how to stitch it all together so they get an e-mail if I make a new or updated post. Voilà, no more being tied to a single platform. I'll be posting those instructions here too, at *[How to get an e-mail from Bill's Blog when a new post is made](https://ToDo) Still in Draft*

## Conclusion

Humans have an innate desire to communicate. I built this blog to communicate. I hope that what I have to say is considered interesting by a large number of folks, and that I'm able to establish a rapport and correspondence with many. I also hope that I can model behavior that encourages others to follow my blog's philosophy and actions.

## Attributions

This content is all mine, no attributions for this post :-)

{% comment %}

the Web Hosting costs me about $13 / month. That includes SQLServer databases and MySql databases, one or more I can activate and integrate with WordPress.

The 1And1 plan also provides an IIS webserver, and space for files. I can put up two domains public facing to the Internet, and as many subdomains of those that could possibly be needed. The fee I pay 1And! includes the ICAN registration abd DNS administration for those domains. I can use my favorite free FTP client, WinSCP, to connect to the 1And1 WebSpace. I have not been able to figure out how to publish there yet.

I used to use Microsoft's Visual Studio  Professional Edition (and pay for it), because I found it was easier to write code and tests from within it. Since retirement and subsequent budget cuts :-), I have switched over to "Visual studio code" with a lot of plugins. I used to pay for CodeRush from DevExpress to help boost my productivity while inside VS, but I switched to using Rider from JetBrains. I like having two IDEs that seem to work well together. There are some tasks that just go easier in VSC and some that are easier in Rider. The dotnet CLI tools, are free, and a Window's Powershell terminal, either inside VSC or standalone, can glue it all together in a script or make a sequence of commands into a one-liner.
{% endcomment %}
