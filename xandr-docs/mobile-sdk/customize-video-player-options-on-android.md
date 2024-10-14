---
title: Customize Video Player Options on Android
description: In this article, find information about the video player controls that you can customize on Android devices.
ms.custom: android-sdk
---

# Customize video player options on Android

`ANVideoPlayerSettings` class lets the publisher app to customize some of the Ad Video Player UI/Controls.

> [!NOTE]
> The customization is applied to all of the Video ads served through Xandr SDK both Instream and Banner Video(Outstream).

| Function | Default Setting | Description | Ad Units supporting the Setting |
|:---|:---|:---|
| `void shouldShowClickThroughControl` <br> (**boolean** `showClickThroughControl`) | true | Determines whether the ClickThrough Control is displayed. Setting it to false makes the entire video clickable. | Instream / Banner Video |
| `void setClickThroughText` <br> (**string** `clickThroughText`) | "Learn More" | Customizes the text associated with the ClickThrough Control. | Instream / Banner Video |
| `void shouldShowFullScreenControl` <br> (**boolean** `showFullScreenControl`)  (Banner Video Only) | true | Controls the visibility of the fullscreen button. |Banner Video|
| `void shouldShowTopBar` <br> (**boolean** `showTopBar`) | true | Determines whether the top bar, containing ClickThrough and Skip controls is displayed. |Instream / Banner Video|
| `void shouldShowAdText` <br> (**boolean** `showAdText`) | true | Controls the visibility of the ad text next to the ClickThrough control. | Instream / Banner Video / Interstitial |
| `void setAdText` <br> (**string** `adText`) | "Ad" | Customizes the ad text on the video player. |Instream / Banner Video / Interstitial|
| `void shouldShowVolumeControl` <br> (**boolean** `showVolumeControl`) | true | Controls the visibility of the mute/unmute control. |Instream / Banner Video|
| `void setInitialAudio` <br> (**ANInitialAudioSetting** `initialAudio`) | Sound On (Instream), Sound Off (Banner Video) | Sets the initial audio state. |Instream / Banner Video|
| `void shouldShowSkip` <br> (**boolean** `showSkip`) (Instream Video Only) | true | Controls the visibility of the Skip control. |Instream / Interstitial|
| `void setSkipDescription` (**String** `skipDescription`) | "Skip in %%TIME%%s" | Customizes Skip Description. | Instream / Interstitial |
| `void setSkipLabelName` (**String** `skipLabelName`) | "Skip ad" | Customizes Skip Label. | Instream / Interstitial |
| `void setSkipOffset` (**Integer** `skipOffset`) | "5 seconds" | Customizes Skip Offset.| Instream / Interstitial |

## Example

### [Java](#tab/java1)

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

### [Kotlin](#tab/kotlin1)

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
