---
title: Customize Video Player Options on iOS
description: In this article, find information about the video player controls that you can customize on iOS SDK.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Customize video player options on iOS

`ANVideoPlayerSettings` class lets the publisher app to customize some of the Ad Video Player UI/Controls.

> [!NOTE]
> The customization is applied to all the Video ads served through Xandr SDK both Instream and Banner Video (Outstream).

| Property | Default Setting | Description |
|---|---|---|
| **BOOL** `showClickThruControl` | true | Determines whether the ClickThrough Control is displayed. Setting it to false makes the entire video clickable |
| **NSString** `*clickThruText` | "Learn More" | Customizes the text associated with the ClickThrough Control |
| **BOOL** `showFullScreenControl` (Banner Video Only) | true | Controls the visibility of the fullscreen button for Banner Video |
| **BOOL** `showTopBar` | true | Determines whether the top bar, containing ClickThrough and Skip controls, is displayed |
| **BOOL** `showAdText` | true | Controls the visibility of the ad text next to the ClickThrough control |
| **NSString** `*adText` | "Ad" | Customizes the ad text on the video player |
| **BOOL** `showVolumeControl` | true | Controls the visibility of the mute/unmute control |
| **ANInitialAudioSetting** `initalAudio` | Sound On (Instream Video), Sound Off ( Banner Video) | Sets the initial audio state for Instream and Banner Videos |
| **BOOL** `showSkip` (Instream Video Only) | true | Controls the visibility of the Skip control for Instream Video |

## Example

### [Objective C](#tab/objectivec1)

```
// Show or Hide the ClickThrough control on the video player. Default is YES, setting it to NO will make the entire video clickable
[[ANVideoPlayerSettings sharedInstance] setShowClickThruControl:NO];

// Change the ClickThrough text on the video player
[[ANVideoPlayerSettings sharedInstance] setClickThruText:@"SampleText"];

// Show or hide fullscreen control on the player. This is applicable only for Banner Video
[[ANVideoPlayerSettings sharedInstance] setShowFullScreenControl:YES];

// Show or hide the top bar that has (ClickThrough & Skip control)
[[ANVideoPlayerSettings sharedInstance] setShowTopBar:YES];

// Show or hide the "Ad" text next to the ClickThrough control
[[ANVideoPlayerSettings sharedInstance] setShowAdText:YES];
[[ANVideoPlayerSettings sharedInstance] setAdText:@"Video Ad"];

// Show or hide the volume control on the player
[[ANVideoPlayerSettings sharedInstance] setShowVolumeControl:YES];

// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
[[ANVideoPlayerSettings sharedInstance] setInitalAudio:Default];
[[ANVideoPlayerSettings sharedInstance] setInitalAudio:SoundOn];
[[ANVideoPlayerSettings sharedInstance] setInitalAudio:SoundOff];

// Show or hide the Skip control on the player
[[ANVideoPlayerSettings sharedInstance] setShowSkip:YES];

// Change the skip description on the video player
[[ANVideoPlayerSettings sharedInstance] setSkipDescription:@"Video Skip Demo"];

// Change the skip button text on the video player
[[ANVideoPlayerSettings sharedInstance] setSkipLabelName:@"Test"];

// Configure the skip offset on the video player
[[ANVideoPlayerSettings sharedInstance] setSkipOffset:2];
```

### [Swift](#tab/swift)

```
// Show or Hide the ClickThrough control on the video player. Default is YES, setting it to NO will make the entire video clickable
ANVideoPlayerSettings.sharedInstance().showClickThruControl = false
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.sharedInstance().clickThruText = "SampleText"
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.sharedInstance().showFullScreenControl = true
 
// Show or hide the top bar that has (ClickThrough & Skip control)
ANVideoPlayerSettings.sharedInstance().showTopBar = true
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.sharedInstance().showAdText = true
ANVideoPlayerSettings.sharedInstance().adText = "Video Ad"
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.sharedInstance().showVolumeControl = true
 
// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
ANVideoPlayerSettings.sharedInstance().initalAudio = ANInitialAudioSetting.Default
ANVideoPlayerSettings.sharedInstance().initalAudio = ANInitialAudioSetting.SoundOn
ANVideoPlayerSettings.sharedInstance().initalAudio = ANInitialAudioSetting.SoundOff
 
// Show or hide the Skip control on the player
ANVideoPlayerSettings.sharedInstance().showSkip = true
 
// Change the skip description on the video player
ANVideoPlayerSettings.sharedInstance().skipDescription = "Video Skip Demo"
 
// Change the skip button text on the video player
ANVideoPlayerSettings.sharedInstance().skipLabelName = "Test"
 
// Configure the skip offset on the video player
ANVideoPlayerSettings.sharedInstance().skipOffset = 2
```
