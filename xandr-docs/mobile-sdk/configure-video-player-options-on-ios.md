---
title: Configure Video Player Options on iOS
description: In this article, find the instructions to customize video player controls on iOS SDK.
ms.custom: ios-sdk
ms.date : 10/28/2023
---

# Configure video player options on iOS

You can customize the following video player controls:

- The clickthrough control
- The mute button
- The fullscreen button for outstream video
- Volume control

**To show or hide the ClickThru control:**

```
@property (nonatomic,assign) BOOL showClickThruControl;
```

The default is YES. NO makes the entire video clickable.

**To change the ClickThru text:**

```
@property (nonatomic, strong) NSString *clickThruText;
```

**To show or hide the fullscreen control (for Banner Video only):**

```
@property (nonatomic,assign) BOOL showFullScreenControl;
```

**To show or hide the top bar (ClickThrough and Skip controls):**

```
@property (nonatomic,assign) BOOL showTopBar;
```

**To show or hide the ad text next to the ClickThru control:**

```
@property (nonatomic,assign) BOOL showAdText;
```

**To change the ad text:**

```
@property (nonatomic, strong) NSString *adText;
```

**To show or hide the volume control:**

```
@property (nonatomic,assign) BOOL showVolumeControl;
```

**To start with video sound on or off:**

```
@property (nonatomic,assign) ANInitialAudioSetting initalAudio;
```

By default, sound will be on for InstreamVideo and off for Banner Video.
