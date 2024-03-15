---
title: Customize Video Player Options on Android
description: In this article, learn instructions and syntax on how to customize video player options on Android devices.
ms.custom: android-sdk
ms.date : 10/28/2023
---

# Customize video player options on Android

You can customize the following video player controls:

- The clickthrough control
- The mute button
- The fullscreen button for outstream video
- Volume control

## Customization samples

To show or hide the ClickThrough control on the video player:

``` 
 private boolean showClickThroughControl = false;
```

The default is true. Setting it to false will make the entire video clickable.

To change the ClickThrough text on the video player:

``` 
 private String clickThroughText = null;
```

To show or hide the fullscreen control (for Banner Video only):

``` 
private boolean showFullScreenControl = false;
```

To show or hide the top bar (ClickThrough and Skip controls):

``` 
 private boolean showTopBar = false;
```

To show or hide the ad text next to the ClickThrough control:

``` 
private boolean showAdText = false;
```

To change the ad text on the video player:

``` 
private String adText = null;
```

To show or hide the volume control:

``` 
 private boolean showVolumeControl = false;
```

To start with video sound on or off:

``` 
private ANInitialAudioSetting initalAudio;
```

By default, sound is on for Instream Video and off for Banner Video.
