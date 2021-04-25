---
Title: Adventures in Voice Diction and Commands for a Developer
tags: Dictation Voice
description: Using Voice Dictation in the development process.
category: technical
---

Voice dictation is the subject of my second blog post 

Specifically, can I switch between dictation mode and programming mode

As I am dictating this into a new voice dictation software package, I have learned just how hard it is to create content on the fly, in complete sentences.

I did an Internet search on the subject of voice commands to/for Visual Studio code. Aside from the usual dross from the big companies, the articles that seemed remotely interesting, all seen to involve one or more third-party packages.

All of the articles suggested that the initial steps are to set up microphone, workspace, and to install a voice recognition app. 

I am familiar with voice recognition on Google, and I have tried Microsoft's Windows built in product.

A few years ago I bought a copy of the commercial version of DragonDictate. I never installed it . But I decided to give it a try today.  The DragonDictate has been bought by Nuance. Looking at their website, there are two newer versions of the software. Not sure I want to spend money on this yet, although one of the Internet article did reference using DragonDictate. Unfortunately the article indicated that the professional version does a much better job. Unfortunately, because it costs significantly more money, and as a retiree, I haven't got any to spare. :-)

Pretty much right out of the box I am dictating all of this into a DragonDictate text control which easily pastes into the notepad++ text editor I'm using.

It has taken me about 10 minutes to dictate all of this, learning as I go. The biggest issue is it doesn't seem to recognize the first couple of words when I start a sentence, so I have to go back to The beginning and enter those words. As happened here, note the capital T prior. I started dictating at "I have to ggo back...".

The next step is to see if it will be possible to give commands to the text editor.

Instead, went down a rabbit hole. Found a forum where people discuss using DragonDictate to control third-party apps. In the forum, I found a few nuggets from people who were, in 2016, using DragonDictate and Visual Studio. What I did see in code examples was that a variation of Basic is being used customized DragonDictate.

My programming language preferences are C# and PowerShell. Realizing that I would have to write significant Visual Basic code, I have decided that DragonDictate is probably not the voice dictation recognition software that I'm looking to pursue.

So it's back to the drawing board! I'll try to write sooner next time.

Combining Voice dictation and code editing is the subject of my third blog post 

(Ed. First paragraph is typed) I was going to try and dictate as I coded, but upon opening my environment, I realized it was time for a housecleaning. I spent a few hours prior to dictating closing out my MAPs subscription cleaning out old SDK versions, removing two of my three Visual studio installs, and creating the first two workspaces for Visual Studio Code in the ATAP.Utilities repository.

So the remainder of this post will be the raw dictation transcription, as I try to get the Powershell code I wrote last week into the original Console program that read a lot of disks, and records info about every file. The next step is to store the data in a graph DB. Yesterday I got the SQL Server 2017(?) service running locally, with the graph extensions, and I also created a node and edge table . I have powershell script that can insert the directory nodes from upstream into the nodes table of the DB

Now to try dictating stream of conscionous to Visual Studio Code

First thing I'm going to try to do is to correct the build tools path.
The solution file contains a section called .build with has entries for tools whose pans include .build from the solution directory.

Hello while I am still trying to figure out why the path to the finished build tools is short by one directory, by manage to move four of the build tools directories under the source parent directory, and was able to properly reroot them in the solution directory under the build folder under src



The second thing I'm going to try to do is to figure out the loft configurations so that it specifies the correct directory.




