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

The `ANVideoPlayerSettings` class lets publisher apps customize some of the ad video player UI controls.



> [!NOTE]
> These settings apply to all video ads served through the Mobile SDK: Instream Video, Banner Video (Outstream), and Interstitial Video.

| Property | Default Setting | Description | Ad Units supporting the Setting |
|:---|:---|:---|:---|
| **BOOL** `showClickThruControl` | true | Determines whether the click-through control is displayed. Setting it to false makes the entire video clickable. | Instream / Banner Video / Interstitial |
| **NSString** `*clickThruText` | "Learn More" | Customizes the text associated with the click-through control. | Instream / Banner Video / Interstitial |
| **BOOL** `showFullScreenControl` | false | Controls the visibility of the full screen button. | Banner Video |
| **BOOL** `showTopBar` | true | **Deprecated:** This property no longer works and will be removed in a future SDK release. | Instream / Banner Video |
| **BOOL** `showAdText` | true | Controls the visibility of the ad text next to the click-through control. | Instream / Banner Video / Interstitial |
| **NSString** `*adText` | "Ad" | Customizes the ad text on the video player. | Instream / Banner Video / Interstitial |
| **BOOL** `showVolumeControl` | true | Controls the visibility of the mute/unmute control. | Instream / Banner Video / Interstitial |
| **ANInitialAudioSetting** `initialAudio` | Sound On (Interstitial / Instream), Sound Off ( Banner Video) | Sets the initial audio state. | Instream / Banner Video / Interstitial |
| **BOOL** `showSkip` | true | Controls the visibility of the Skip control. | Instream / Interstitial |
| **NSString** `*skipDescription` | "Skip ad in %%TIME%%" | Customizes Skip Description. | Instream / Interstitial |
| **NSString** `*skipLabelName` | "Skip ad" | Customizes Skip Label. | Instream / Interstitial |
| **NSInteger** `*skipOffset` | "5 seconds" | Customizes Skip Offset. | Instream / Interstitial |
| **BOOL** `forceControlBarVisible` | true | When set to `true`, the video control bar (play/pause, seek, volume, and other controls) remains permanently visible, regardless of user interaction.<br> When set to `false`, the player uses the auto-hide behavior, where the control bar hides after a period of inactivity. | Instream / Banner Video / Interstitial |
| **BOOL** `clickBehaviorPausePlay` | true | When set to `true` (default), clicking or tapping the video toggles pause/play. When set to `false`, taps are passed to other handlers (for example, click-through). | Instream / Banner Video / Interstitial |

## Example

### [Objective C](#tab/objectivec1)

```
// Show or hide the ClickThrough control on the video player. Default is YES; setting it to NO makes the entire video clickable
[[ANVideoPlayerSettings sharedInstance] setShowClickThruControl:NO];

// Change the ClickThrough text on the video player
[[ANVideoPlayerSettings sharedInstance] setClickThruText:@"SampleText"];

// Show or hide fullscreen control on the player. This is applicable only for Banner Video
[[ANVideoPlayerSettings sharedInstance] setShowFullScreenControl:YES];

// Deprecated: this property is no longer functional and will be removed in a future SDK version
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

// When set to YES (default), tapping the video toggles pause/play. Set to NO to pass taps to other handlers (e.g. click-through)
[ANVideoPlayerSettings sharedInstance].clickBehaviorPausePlay = NO;

// Change the skip description on the video player
[[ANVideoPlayerSettings sharedInstance] setSkipDescription:@"Video Skip Demo"];

// Change the skip button text on the video player
[[ANVideoPlayerSettings sharedInstance] setSkipLabelName:@"Test"];

// Configure the skip offset on the video player. Minimum value is 5 seconds; lower values are clamped to 5
[[ANVideoPlayerSettings sharedInstance] setSkipOffset:2];
```

### [Swift](#tab/swift)

```
// Show or hide the ClickThrough control on the video player. Default is true; setting it to false makes the entire video clickable
ANVideoPlayerSettings.sharedInstance().showClickThruControl = false
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.sharedInstance().clickThruText = "SampleText"
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.sharedInstance().showFullScreenControl = true
 
// Deprecated: this property is no longer functional and will be removed in a future SDK version
ANVideoPlayerSettings.sharedInstance().showTopBar = true
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.sharedInstance().showAdText = true
ANVideoPlayerSettings.sharedInstance().adText = "Video Ad"
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.sharedInstance().showVolumeControl = true

// Show or hide the control bar permanently (default is true to always show). If set to false, the player will auto-hide the control bar after inactivity.
ANVideoPlayerSettings.sharedInstance().forceControlBarVisible = false

// When set to true (default), tapping the video toggles pause/play. Set to false to pass taps to other handlers (e.g. click-through)
ANVideoPlayerSettings.sharedInstance().clickBehaviorPausePlay = false
 
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
 
// Configure the skip offset on the video player. Minimum value is 5 seconds; lower values are clamped to 5
ANVideoPlayerSettings.sharedInstance().skipOffset = 2
```
