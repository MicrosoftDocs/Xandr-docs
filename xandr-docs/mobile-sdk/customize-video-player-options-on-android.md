---
title: Customize Video Player Options on Android
description: In this article, find information about the video player controls that you can customize on Android devices.
ms.custom: android-sdk
ms.date : 10/28/2023
---

# Customize video player options on Android

`ANVideoPlayerSettings` class allows publisher app to customize some of the Ad Video Player UI/Controls.

> [!NOTE]
> The customization is applied to all of the Video ads served through Xandr SDK both Instream and Banner Video(Outstream).

| Parameter | Type | Default Setting | Description |
|--|--|--|--|
| `showClickThroughControl` | boolean | true | Determines whether the ClickThrough Control is displayed. Setting it to false makes the entire video clickable. |
| `clickThroughText` | String | "Learn More" | Customizes the text associated with the ClickThrough Control. |
| `showFullScreenControl` (Banner Video Only) | boolean | true | Controls the visibility of the fullscreen button for Banner Video. |
| `showTopBar` | boolean | true | Determines whether the top bar, containing ClickThrough and Skip controls, is displayed. |
| `showAdText` | boolean | true | Controls the visibility of the ad text next to the ClickThrough control. |
| `adText` | String | "Ad" | Customizes the ad text on the video player. |
| `showVolumeControl` | boolean | true | Controls the visibility of the mute/unmute control. |
| `initialAudio` | ANInitialAudioSetting | Sound On (Instream), Sound Off ( Banner Video) | Sets the initial audio state for Instream and Banner Videos. |
| `showSkip` (Instream Only) | boolean | true | Controls the visibility of the Skip control for Instream Video. |

## Example

### [Java](#tab/java)

```
// Show or Hide the ClickThrough control on the video player. Default is YES, setting it to NO will make the entire video clickable
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowClickThroughControl(false);
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setClickThroughText("SampleText");
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowFullScreenControl(true);
 
// Show or hide the top bar that has (ClickThrough & Skip control)
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowTopBar(true);
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowAdText(true);
ANVideoPlayerSettings.getVideoPlayerSettings().setAdText("Video Ad");
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowVolumeControl(true);
 
// Decide how the ad video sound starts initially (sound on or off). By default, Instream Video will have sound enabled, while Banner Video will have sound disabled
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(DEFAULT);
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(SOUND_ON);
ANVideoPlayerSettings.getVideoPlayerSettings().setInitialAudio(SOUND_OFF);
 
// Show or hide the Skip control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowSkip(true);
 
// Change the skip description on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipDescription("Video Skip Demo");
 
// Change the skip button text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipLabelName("Test");
 
// Configure the skip offset on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().setSkipOffset(2);
```

### [Kotlin](#tab/kotlin)

```
// Show or Hide the ClickThrough control on the video player. Default is YES, setting it to NO will make the entire video clickable
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowClickThroughControl(false)
 
// Change the ClickThrough text on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().clickThroughText = "SampleText"
 
// Show or hide fullscreen control on the player. This is applicable only for Banner Video
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowFullScreenControl(true)
 
// Show or hide the top bar that has (ClickThrough & Skip control)
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowTopBar(true)
 
// Show or hide the "Ad" text next to the ClickThrough control
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowAdText(true)
ANVideoPlayerSettings.getVideoPlayerSettings().adText = "Video Ad"
 
// Show or hide the volume control on the player
ANVideoPlayerSettings.getVideoPlayerSettings().shouldShowVolumeControl(true)
 
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
 
// Configure the skip offset on the video player
ANVideoPlayerSettings.getVideoPlayerSettings().skipOffset = 2
```
