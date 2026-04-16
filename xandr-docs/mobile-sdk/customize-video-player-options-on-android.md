---
title: Customize Video Player Options on Android
description: In this article, find information about the video player controls that you can customize on Android devices.
ms.custom: android-sdk
ms.date: 3/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Customize video player options on Android

The `ANVideoPlayerSettings` class lets publisher apps customize some of the ad video player UI controls.

> [!NOTE]
> These settings apply to all video ads served through the Mobile SDK: Instream Video, Banner Video (Outstream), and Interstitial Video.

| Function | Default Setting | Description | Ad Units supporting the Setting |
|:---|:---|:---|:---|
| `void shouldShowClickThroughControl(boolean showClickThroughControl)` | true | Determines whether the click-through control is displayed. Setting it to false makes the entire video clickable. | Instream / Banner Video / Interstitial |
| `void setClickThroughText(String clickThroughText)` | "Learn More" | Customizes the text associated with the click-through control. | Instream / Banner Video / Interstitial |
| `void shouldShowFullScreenControl(boolean showFullScreenControl)` | true | Controls the visibility of the full screen button. |Banner Video|
| `void shouldShowTopBar(boolean showTopBar)` | true | **Deprecated.** Determines whether the top bar (which contains the click-through and skip controls) is displayed. This method is no longer functional and will be removed in a future SDK version. |Instream / Banner Video|
| `void shouldShowAdText(boolean showAdText)` | true | Controls the visibility of the ad text next to the click-through control. | Instream / Banner Video / Interstitial |
| `void setAdText(String adText)` | "Ad" | Customizes the ad text on the video player. |Instream / Banner Video / Interstitial|
| `void shouldShowVolumeControl(boolean showVolumeControl)` | true | Controls the visibility of the mute/unmute control. | Instream / Banner Video / Interstitial |
| `void setInitialAudio(ANInitialAudioSetting initialAudio)` | Sound On (Interstitial / Instream), Sound Off (Banner Video) | Sets the initial audio state. | Instream / Banner Video / Interstitial |
| `void shouldShowSkip(boolean showSkip)` | true | Controls the visibility of the Skip control. |Instream / Interstitial|
| `void setSkipDescription` (**String** `skipDescription`) | "Skip ad in %%TIME%%" | Customizes Skip Description. | Instream / Interstitial |
| `void setSkipLabelName` (**String** `skipLabelName`) | "Skip ad" | Customizes Skip Label. | Instream / Interstitial |
| `void setSkipOffset` (**Integer** `skipOffset`) | "5 seconds" | Customizes Skip Offset.| Instream / Interstitial |
| `void shouldForceControlBarVisible` (**boolean** `forceControlBarVisible`)| true | When set to `true`, the video control bar (play/pause, seek, volume, and other controls) remains permanently visible, regardless of user interaction.<br> When set to `false`, the player uses the auto-hide behavior, where the control bar hides after a period of inactivity.| Instream / Banner Video / Interstitial |
| `void shouldClickBehaviorPausePlay(boolean clickBehaviorPausePlay)` | true | When set to `true` (default), clicking or tapping the video toggles pause/play. When set to `false`, clicks are passed to other handlers (for example, click-through). | Instream / Banner Video / Interstitial |

## Example

### [Java](#tab/java1)

```
// Show or hide the ClickThrough control on the video player. Default is true; setting it to false makes the entire video clickable
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowClickThroughControl(false);
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setClickThroughText("SampleText");
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowFullScreenControl(true);
 
// Deprecated: this method is no longer functional and will be removed in a future SDK version
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowTopBar(true);
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowAdText(true);
ANVideoPlayerSettings.getVideoPlayerSettings().setAdText("Video Ad");
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowVolumeControl(true);
 
// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(ANInitialAudioSetting.DEFAULT);
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(ANInitialAudioSetting.SOUND_ON);
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(ANInitialAudioSetting.SOUND_OFF);
 
// Show or hide the Skip control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowSkip(true);
 
// Change the skip description on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipDescription("Video Skip Demo");
 
// Change the skip button text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipLabelName("Test");
 
// Configure the skip offset on the video player. Minimum value is 5 seconds; lower values are clamped to 5
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipOffset(2);

// Show or hide the control bar permanently (default is true to always show). If set to false, the player will auto-hide the control bar after inactivity.
ANVideoPlayerSettings.getVideoPlayerSettings().shouldForceControlBarVisible(false);

// When set to true (default), clicking the video toggles pause/play. Set to false to pass clicks to other handlers (e.g. click-through)
ANVideoPlayerSettings.getVideoPlayerSettings().shouldClickBehaviorPausePlay(false);

```

### [Kotlin](#tab/kotlin1)

```
// Show or Hide the ClickThrough control on the video player. Default is YES, setting it to NO will make the entire video clickable
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowClickThroughControl(false)
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().clickThroughText = "SampleText"
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowFullScreenControl(true)
 
// Deprecated: this method is no longer functional and will be removed in a future SDK version
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowTopBar(true)
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowAdText(true)
ANVideoPlayerSettings.getVideoPlayerSettings().adText = "Video Ad"
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowVolumeControl(true)

// Show or hide the control bar permanently (default is true to always show). If set to false, the player will auto-hide the control bar after inactivity.
ANVideoPlayerSettings.getVideoPlayerSettings().shouldForceControlBarVisible(false)

// When set to true (default), clicking the video toggles pause/play. Set to false to pass clicks to other handlers (e.g. click-through)
ANVideoPlayerSettings.getVideoPlayerSettings().shouldClickBehaviorPausePlay(false)
 
// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
ANVideoPlayerSettings.getVideoPlayerSettings().initialAudio = ANInitialAudioSetting.DEFAULT
ANVideoPlayerSettings.getVideoPlayerSettings().initialAudio = ANInitialAudioSetting.SOUND_ON
ANVideoPlayerSettings.getVideoPlayerSettings().initialAudio = ANInitialAudioSetting.SOUND_OFF
 
// Show or hide the Skip control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowSkip(true)
 
// Change the skip description on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().skipDescription = "Video Skip Demo"
 
// Change the skip button text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().skipLabelName = "Test"
 
// Configure the skip offset on the video player. Minimum value is 5 seconds; lower values are clamped to 5
ANVideoPlayerSettings.getVideoPlayerSettings().skipOffset = 2
```
