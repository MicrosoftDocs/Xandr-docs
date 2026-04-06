---
title: Customize Video Player Options on iOS
description: In this article, find information about the video player controls that you can customize on iOS SDK.
ms.custom: ios-sdk
ms.date: 3/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Customize video player options on iOS

`ANVideoPlayerSettings` class lets the publisher app to customize some of the Ad Video Player UI/Controls.



> [!NOTE]
> The customization is applied to all the Video ads served through Xandr SDK both Instream, Banner Video (Outstream) and Interstitial Video.

| Property | Default Setting | Description | Ad Units supporting the Setting |
|---|---|---|
| **BOOL** `showClickThruControl` | true | Determines whether the ClickThrough Control is displayed. Setting it to false makes the entire video clickable. | Instream/Banner Video |
| **NSString** `*clickThruText` | "Learn More" | Customizes the text associated with the ClickThrough Control. |Instream/Banner Video |
| **BOOL** `showFullScreenControl` (Banner Video Only) | false | Controls the visibility of the fullscreen button. | Banner Video |
| **BOOL** `showTopBar` | true | **Deprecated.** Determines whether the top bar, containing ClickThrough and Skip controls, is displayed. This property is no longer functional and will be removed in a future SDK version. | Instream/Banner Video |
| **BOOL** `showAdText` | true | Controls the visibility of the ad text next to the ClickThrough control. | Instream/Banner Video/Interstitial |
| **NSString** `*adText` | "Ad" | Customizes the ad text on the video player. | Instream/Banner Video/Interstitial |
| **BOOL** `showVolumeControl` | true | Controls the visibility of the mute/unmute control. | Instream/Banner Video |
| **ANInitialAudioSetting** `initialAudio` | Sound On (Instream Video), Sound Off ( Banner Video) | Sets the initial audio state. | Instream/Banner Video |
| **BOOL** `showSkip` | true | Controls the visibility of the Skip control. | Instream |
| **NSString** `*skipDescription` | "Skip ad in %%TIME%%" | Customizes Skip Description. | Instream |
| **NSString** `*skipLabelName` | "Skip ad" | Customizes Skip Label. | Instream |
| **NSInteger** `*skipOffset` | "5 seconds" | Customizes Skip Offset. | Instream |
| **BOOL** `forceControlBarVisible` | true | When set to `true`, the video control bar (play/pause, seek, volume, and other controls) remains permanently visible, regardless of user interaction. When set to `false`, the player uses the auto-hide behavior, where the control bar hides after a period of inactivity. | Instream/Banner Video/Interstitial |

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
[[ANVideoPlayerSettings sharedInstance] setInitialAudio:Default];
[[ANVideoPlayerSettings sharedInstance] setInitialAudio:SoundOn];
[[ANVideoPlayerSettings sharedInstance] setInitialAudio:SoundOff];

// Show or hide the Skip control on the player
[[ANVideoPlayerSettings sharedInstance] setShowSkip:YES];

// Show or hide the control bar permanently (default is YES to always show). If set to NO, the player will auto-hide the control bar after inactivity.
[ANVideoPlayerSettings sharedInstance].forceControlBarVisible = NO;

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

// Show or hide the control bar permanently (default is true to always show). If set to false, the player will auto-hide the control bar after inactivity.
ANVideoPlayerSettings.sharedInstance().forceControlBarVisible = false
 
// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
ANVideoPlayerSettings.sharedInstance().initialAudio = ANInitialAudioSetting.Default
ANVideoPlayerSettings.sharedInstance().initialAudio = ANInitialAudioSetting.SoundOn
ANVideoPlayerSettings.sharedInstance().initialAudio = ANInitialAudioSetting.SoundOff
 
// Show or hide the Skip control on the player
ANVideoPlayerSettings.sharedInstance().showSkip = true
 
// Change the skip description on the video player
ANVideoPlayerSettings.sharedInstance().skipDescription = "Video Skip Demo"
 
// Change the skip button text on the video player
ANVideoPlayerSettings.sharedInstance().skipLabelName = "Test"
 
// Configure the skip offset on the video player
ANVideoPlayerSettings.sharedInstance().skipOffset = 2
```
