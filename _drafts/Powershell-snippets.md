---
Title: Powershell snippets
tags: Powershell
layout: post
description: Useful snippets of Powershell 
category: technical
---

Get-ChildItem -File -r | where {$_.fullname -match "cshtml"}| foreach { git mv ($_.fullname) ($_.fullname –replace "cshtml","razor") }

Get-ChildItem -Dir -r | where {$_.fullname -match "obj|bin"} | foreach {$_.fullname}

