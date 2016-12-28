---
layout: post
title: "iOS: Use Music Library With Simulator
"
description: ""
category: 
tags: [iOS, XCode]
---
{% include JB/setup %}

### Music in the Simulator
When you are building a music player application it is general believe that you will have to test this on an actual device since you can't access your music library on the simulator.  
However this isn't true, there is a way to test this on the simulator. It will require some work tho.

#### Requirements
 - An device with a music library on it
 - [iFunBox](http://www.i-funbox.com)
 - The id of the simulator you want to test this on

#### How To  
Now we will go into how you will actually get this working.  
First you will need to know that you can not do this in one swoop for every simulator.  
Every device in the simulator has it's own id and is in fact it's own device.  
If you want to be able to access the music library you will have to do this for **every single device** you require this to work on.

What we will be doing is copying the entire music library from your phone to the simulator which will allow us to use this inside the simulator.  
**It might be smart** to resync your phone with only a few songs/albums so you won't be dealing with over 22GB in music.

First you will need to know what the id of the simulator is.
```bash
xcrun simctl list
```

Will return a list that will tell you every id of every device
```bash  
== Devices ==
-- iOS 10.2 --
    iPhone 5 (8E173D11-B725-4966-B525-xxxx) (Shutdown)
    iPhone 5s (FEF4993D-DF5A-4802-B543-xxxx) (Shutdown)
    iPhone 6 (F215D467-A0C9-433D-AB7B-xxxx) (Shutdown)
    iPhone 6 Plus (E99E1067-CFB3-43E5-83C8-xxxx) (Shutdown)
    iPhone 6s (9CC159E4-C572-4CE8-978C-xxxx) (Shutdown)
    iPhone 6s Plus (2727C37D-2CB9-4F0C-xxxx) (Shutdown)
    iPhone 7 (8A14CCDB-6AEE-49FA-B65F-xxxx) (Booted)
    iPhone 7 Plus (7C19745F-4FE6-44AD-94A7-xxxx) (Shutdown)
    iPhone SE (BA0F4C31-A0FB-4465-93E9-xxxx) (Shutdown)
    iPad Retina (B2A34246-901C-4C4F-824C-xxxx) (Shutdown)
    iPad Air (57135CCC-1117-40C1-8D43-xxxx) (Shutdown)
    iPad Air 2 (E42EBC0D-EF02-4A02-8190-xxxx) (Shutdown)
    iPad Pro (9.7 inch) (CEF665A1-4CD7-4C66-B774-xxxx) (Shutdown)
    iPad Pro (12.9 inch) (1D611039-1208-4D65-94E6-xxxx) (Shutdown)
-- tvOS 10.1 --
    Apple TV 1080p (94E65157-CC59-4BB5-801D-xxxx) (Shutdown)
-- watchOS 3.1 --
    Apple Watch - 38mm (62FEA43E-521E-4BFD-A9BB-xxxx) (Shutdown)
    Apple Watch - 42mm (0686C55C-9E2B-4208-927D-xxxx) (Shutdown)
    Apple Watch Series 2 - 38mm (8DB7FD6C-0D44-4ED1-85EB-xxxx) (Shutdown)
    Apple Watch Series 2 - 42mm (19A73926-2506-452E-8196-xxxx) (Shutdown)
-- Unavailable: com.apple.CoreSimulator.SimRuntime.iOS-10-1 --
    iPhone 5 (D03CCA6F-5E98-4E48-9582-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 5s (F61B5E14-D296-4679-8D91-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 6 (2A92FC53-AFB4-4C46-AFCB-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 6 Plus (B986B9A4-361C-490E-A7ED-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 6s (E3CE12AB-5DB2-4731-B4EB-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 6s Plus (7C68DCC1-F4F6-4ABE-8C58-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPhone 7 (392550E5-7FFA-4173-A98F-xxxx) (Creating) (unavailable, runtime profile not found)
    iPhone 7 Plus (913969FA-9D72-427B-900D-xxxx) (Creating) (unavailable, runtime profile not found)
    iPhone SE (282C2416-CE56-4B93-9856-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPad Retina (0A62734E-7770-4B9F-9B56-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPad Air (87C237B6-F7EB-4EF6-AC40-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPad Air 2 (438F5D25-8C65-4FA4-869F-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPad Pro (9.7 inch) (F10F8EE6-6B96-4C26-AFB1-xxxx) (Shutdown) (unavailable, runtime profile not found)
    iPad Pro (12.9 inch) (2F35AAF4-8D34-4969-BD82-xxxx) (Shutdown) (unavailable, runtime profile not found)
```

Take down the ID of the device you require.

Next we will actually navigate to the directory of this device.

```bash  
[yourHD] -> Users -> [yourusername] -> Library -> Developer -> CoreSimulator -> Devices -> [the ID you obtained in the previous step] -> data -> Media -> Itunes_Control -> Itunes
```

Leave this directory open as you will need it in the next step.

Next up we will open the `iFunBox` application, you will need to connect your phone to your computer for this as `iFunBox` will allow is to look into the directories of your iPhone.  
When you've opened iFunBox you will need to select `Raw File System`. 
In here you will find the directory `Itunes_Connect`

<img src="/assets/img/ifunbox.png" width="600px" />

From that directory on you will need to copy the following directories and files to the simulator directory you opened in the previous step
```
Music
iTunes/Artwork
iTunes/MediaLibrary.sqlitedb
iTunes/MediaLibrary.sqlitedb-shm
iTunes/MediaLibrary.sqlitedb-wal
```

If you ever bought music you should also grab the following directory
```
Raw File System/Purchases
```

That's it you should now be able to open your application and see the music files appear. You should even be able to play them!  
<img src="/assets/img/result.png" width="600px" />