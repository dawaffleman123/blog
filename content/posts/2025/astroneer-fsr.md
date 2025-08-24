---
title: "How To Set Up FSR on Astroneer With Proton on Linux "
date: 2025-07-16
draft: false
tags:
  - linux
  - games
categories:
  - Tutorials
---

## How To Set Up FSR on Astroneer With Proton on Linux


My laptop of choice is the Framework 16 with no dedicated graphics. This means that I have to play at low framerates settings. With the magic of FSR which allows me to run the game at a lower resolution and use the gpu to upscale it I am able to get higher refresh rates on the same settings. Typically the process involves adding some settings in steam and making the game fullscreen and lowering the in-game resolution.

However Astroneer does not have a fullscreen mode. So we have to change some settings manually.
## Install ProtonGE through ProtonUp-Qt

Depending on your distribution it will be different, I use Fedora so I had to install it as a flatpak.
![ProtonUp-Qt](/images/2025/astroneer-fsr/proton-up.png)
**YOU WILL NEED TO CLOSE STEAM TO CONTINUE**
#### Select Your Steam Package If Not Automatic


This should select your steam version automatically but verify that it is the correct one.
#### Install The Latest ProtonGE Version


Press **Add Version**
![Add Version](/images/2025/astroneer-fsr/p1.png)

Select the most recent version of **GE-Proton** and press **Install**
## Open Steam And Select Astroneer

Click the settings button on the game and go to properties
#### Enable FSR
This works for all games but under launch option add

    WINE_FULLSCREEN_FSR=1 %command%
## Change The Compatibility Tool


1. Go to the compatibility tab and check **Force the use of a specific Steam Play compatibility tool**

2. Then select the version of **GE-Proton** you have

It should look like the following
![Compatibility Page](/images/2025/astroneer-fsr/p2.png)

## Edit GameUserSettings.ini To Force Fullscreen


Because Astroneer will not let us set fullscreen manually we have to force it with a file.
#### Find the file

1. Go to **Installed Files** and press **Browse…**
2. Click back to steamapps
    ![steamapps](/images/2025/astroneer-fsr/a1.png)
3. Open `compatdata/361420/pfx/drive_c/users/steamuser/AppData/Local/Astro/Saved/Config/WindowsNoEditor/GameUserSettings.ini`

## Edit the following values
| Setting |	What it does |
| ------- | ------------ |
| `ResolutionSizeX` |	The width of your monitor |
| `ResolutionSizeY` |	The height of your monitor |
| `LastUserConfirmedResolutionSizeX` |	Set this to the same as `ResolutionSizeX` |
| `LastUserConfirmedResolutionSizeY` |	Set this to the same as `ResolutionSizeY` |
| `FullscreenMode` |	`0` means exclusive fullscreen,` 1` is borderless, `2` is windowed |
| `LastConfirmedFullscreenMode` |	Set this to the same as `FullscreenMode` |
| `PreferredFullscreenMode` |	Set this to the same as `FullscreenMode` |

Here is my file for reference
``` ini
ResolutionSizeX=1280
ResolutionSizeY=800
LastUserConfirmedResolutionSizeX=1280
LastUserConfirmedResolutionSizeY=800
WindowPosX=-1
WindowPosY=-1
FullscreenMode=0
LastConfirmedFullscreenMode=0
PreferredFullscreenMode=0
```
## Launch The Game

It should work if not send me an email below and I can update the article