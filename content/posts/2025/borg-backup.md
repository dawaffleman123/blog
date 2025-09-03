---
title: "Setting Up Backups with BORG"
date: 2025-08-25
draft: true
tags:
  - linux
  - servers
categories:
  - Tutorials
---

# Setting Up Borg Backup with Vorta

> "An NVME SSD will never fail, trust me bro I have been running the same one for years" - Brady Van Oss

## Welcome Back To School Fail

Typically when being welcomed back to school there is free hand outs, food, sales on random office supplies I'll never find a use for and, the excitement of starting a new year. I did not expect however, complete SSD failure. 

I liked to believe that drive failure was predictable, a set limit that you could write to it then it would fail, or a SMART test that would conviently go off to let me know of my impending doom. I can now confidently state that this is not the case and the whole drive will just kill itself. I tried everything to get my data back but to no avail, clonezilla gave me errors preventing me from reading the disk for over half of the 2TB that I had.

I had a partial backup that I had made to a different server but it was still missing some of my files. I had even lost the blog files and had to re-do the whole thing using only the stuff available online (I have learned my lesson and now use github). Going forward I knew the system I had that was "Do whatever I want until something breaks" would not cut it, I had to find a better solution

## Finding the perfect backup solution
I looked at many programs at first, starting with rclone. It was something that I was familiar with and I knew that it would satisfy my needs. It had an option too where it would only upload the files that were new or changed. This lacked some major features however, no compression and no ability to go back and have a history of my files.

Continuing my search I found UrBackup and duplicati but these faced their own issues, UrBackup could make full ISO backups on windows but not linux and support for the project seemed spotty at best. Duplicati appeared to be too resource intensive (though I did use it on my windows machine) but lacked the speed and compression of my next option.

## Assimilating with the BORG
BORG Backup, unrelated to the Star Trek referance, is a *Deduplicating archiver with compression and encryption* - [BORG](https://www.borgbackup.org/). This program solved all my problems and because it was open source and well maintained guis have been developed for it making it easy for laptop use. The primary one that I use is called [Vorta](https://vorta.borgbase.com/).

# Setting up Vorta with NFS
