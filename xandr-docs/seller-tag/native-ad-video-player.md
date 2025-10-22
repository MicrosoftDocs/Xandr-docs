---
title: Native Ad Video Player
description: In this article, explore the features of the Native Ad Video Player, its API entry points and player options, and how to invoke this player with a detailed example.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Native ad video player

**The Native Ad Video Player** is an implementation of the Xandr Vast Player designed to be used within the Xandr Native Renderer for use with Native Ads.

## Features

The Xandr Vast Player is designed to provide the following features:

- Plays an ad video as delivered in VAST XML.
- You can pass the player the VAST XML in one of the following forms:  
  - URL to a valid VAST XML
  - Direct VAST XML content
- Optionally, displays an pre-show banner image before the ad video plays.
- Optionally, displays a post-show banner image after the ad video plays.
- Optionally, supports a click through if the user clicks on the post-show banner image.
- Optionally, reports a click tracking event if the user clicks on the post-show image.

## API entry point

To get the player to play the native video, you must utilize the `playNativeAdVideo` function. This function passes `targetDiv`, `vast`, `options`, `bannerOptions`, and  `notificationCallback` as arguments.

### Arguments

| Argument | Description | Acceptable Values | Required | Default |
|:---|:---|:---|:---|:---|
| `targetDiv` | The HTML DIV element that contains the ad player. | DIV element that is present on the page. | Yes | None |
| `vast` | String which provides the source of the VAST xml. This can be either the url to the VAST xml or the VAST xml itself.<br>If the VAST xml defines a video ad, then the ad will play. | String that represents one of the following:<br> - A valid URL which will return valid VAST xml.<br> - A VAST xml document. | Yes | None |
| `options` | Contains the set of configuration options for the player. | Javascript object which includes one or more of the supported [Player Options](#player-options) listed below. | Yes, but the object can be empty. | None |
| `bannerOptions` | Contains the set of banner-related options for the video player.<br>You can use any type of image that can be used as a background of a DOM element. | Javascript object which includes one or more the following fields.<br> - `preBanner`  (String) - required - Specifies the url to an image that will be displayed before the video plays.<br><br> - `postBanner`   (String) - optional<br>&nbsp; - Specifies the url to an image that will be displayed after the video plays.<br>&nbsp; - If it is not specified, then the preBanner image will also be displayed after the video plays.<br><br> - `clickUrl`  (String) - optional<br>&nbsp; - Specifies the url to the landing page that will be used when the user clicks on the postBanner image is clicked.<br><br> - `trackingUrl`   (String) - optional<br>&nbsp; - Specifies the tracking url that will be reported when the user clicks on the postBanner image is clicked.<br>&nbsp; - If the clickUrl is not specified, then this option will be ignored. | Yes | None |
| `notificationCallback` | Callback that the player will call with status information about the playback of the ad. | Function which has the prototype defined below in the [Notification Callback](#notification-callback). | No | Undefined |

## How to invoke?

The Xandr Native Ad Renderer should do the following to use the Native Ad Video Player within a native ad:

1. Load the Xandr Vast Player. The Xandr Vast Player will automatically assign the player a variable named `APNVideo_VastVideoPlayer` which will be globally available within the Renderer's document window.
1. Create the div where the player will be located.
1. Construct the set of parameters that need to be passed into the native video player:
    1. A reference to the target div element where the player is located, as create in Step \#2.
    1. Either the url to the target VAST xml or a String containing the VAST xml document itself.
    1. A Javascript object containing the set of player options which control the rendering of the video ad itself. For the list of rendering options supported, see [Player Options](#player-options).
    1. A Javascript object containing the set of banner options to be enforced by the native video player. These include:

          1. `preBanner` - image url (optional).
          1. `postBanner` - image url (optional).
          1. `clickUrl` - landing page when clicking on the postBanner (optional).
          1. `trackingUrl` - tracking url to report the click on the postBanner (optional).
    1. An optional `notificationCallback` function which the player will use to report status.
1. Initiate the Native Ad Video Player by calling the API entry point cited above.

### Example

```
// Code has to be located within same document where the Native Renderer is located
  
// this will load the player and automatically create the APNVideo_VastVideoPlayer variable
var scr = document.createElement('script');
scr.type = 'text/javascript';
scr.src = ‘//acdn.adnxs.com/video/player/vastPlayer/XandrVastPlayer.js’;
document.getElementsByTagName('head')[0].appendChild(scr);
 
 
// once you know that the player has been loaded and you are ready to use it:
var targetDiv = document.getElementById(‘playerContainer’;
var options = {skippable : {enabled: false}};
var vastUrl = ‘http://path-to-my-xml.xml’;
 
var bannerOptions = {};
bannerOptions.preBanner = 'http://my-path-preshow.jpg';
bannerOptions.postBannder = 'http://my-path-postshow.jpg';
bannerOptions.clickUrl = 'http://my-fake-page.com';
bannerOptions.trackingUrl = 'http://my-tracking-url.jpg';
 
APNVideo_VastVideoPlayer.playNativeAdVideo(targetDiv, vastUrl, options, bannerOptions, function(eventCode, data) {console.log ("Native Notified: " + eventCode);});
```

## Player options

Player options are passed into the Xandr Video Player in a Javascript object. The following options are supported:

| Field Name | Description | Acceptable Values | Is Required | Default | Example |
|:---|:---|:---|:---|:---|:---|
| `initialPlayback` | Specifies whether the ad video requires a click to start or whether it should autoplay without a user click.<br><br>**Note:** Most browsers and mobile devices do not permit a video to autoplay with the sound on. Most browsers and devices require a user click if the audio is on. If a browser or device detects that the video is configured to autoplay with sound on, the browser or device will enforce the use of a user click to start the video. | String which can be one of the following:<br>- `auto`: The video will automatically start to play once it is loaded; no user click is needed to start the video.<br> - `click`: The video requires a click to start its playback; usually a play button is displayed inviting the user to click it to start the video. | No | 'click' | `initalPlayback : 'auto'` |
| `initialAudio` | Specifies whether the audio of the ad video is audible at video start or the audio is muted.<br>Users usually have the option to enable the audio if the video starts in a muted state. Users also usually have the option to mute the audio if the video starts with the audio on.<br><br>**Note:** Most browsers and mobile devices do not permit a video to autoplay with the sound on. Most browsers and devices require a user click if the audio is on. If a browser or device detects that the video is configured to autoplay with sound on, the browser or device will enforce the use of a user click to start the video.<br><br>For most click-to-play cases, you would use following settings:<br>`initialPlayback : 'click';`<br>`initialAudio : 'on'`<br>For most autoplay cases, it is recommended that you use:<br>`initialPlayback : 'auto';`<br>`initialAudio : 'off'` | String which can be one of the following:<br>- `on`: The audio of the video will be audible when the video starts.<br> - `off`: The audio of the video will be muted when the video starts. | No | 'on' | `initialAudio: 'off'` |
| `skippable` | Specifies the publisher's preferred handling of the SKIP button. <br><br>**Note:** Skippable behavior is disabled by default for the Native Ad Video Player.<br><br>Use the skippable options to modify the default behaviors. | JSON Object which can contain the following fields:<br><br> - `enabled` = boolean where true = support skippable behavior and false = turn off skippable behavior; default value is false.<br><br> - `videoThreshold` = (number) minimum length of the ad video in seconds to show the skip button. If the ad video is shorter than this threshold, then NO skip button will be shown. Default value is 15 seconds.<br><br> - `videoOffset` = (number) how long to wait in seconds before showing the skip button. Default value is 5 seconds.<br><br> - `skipLocation` = string specifying the position of the skip button; can be "top-left" (default) or "top-right".<br><br> - `skipText` = (string) text to display announcing the ability to skip the ad; Use %%TIME%% to insert the remaining time.  Default value: <br>&nbsp; - For video ads: "Video can be skipped in %%TIME%% seconds".<br>&nbsp; - For audio ads: "Audio can be skipped in %%TIME%% seconds."<br><br> - `skipButtonText` = string specify the text of the Skip Button; default = "SKIP". | No | {} | `skippable : {`<br>    `enabled :  false,`<br>    `videoThreshold : 30,`<br>    `videoOffset : 15`<br>`}` |
| `adStartTimeout` | Maximum time in milliseconds that the player will wait for the ad to start. | Number | NO | 5000 | `adStartTimeout: 6000` |
| `adServerTimeout` | Maximum time in milliseconds that the player will wait to retrieve a response when calling an ad server, especially important during the parsing of the VAST xml. <br><br>**Note:**  `adServerTimeout`  should not be greater than the value for  `adStartTimeout`. If you need to greatly increase the limit for  `adServerTimeout`  to greater than the default value for  `adStartTimeout`, then you should also increase the value of  `adStartTimeout`. | Number | No | 2000 | `adServerTimeout: 4000` |
| `adText` | String specifying the text used in the ad indicator in the top bar of the ad player.<br><br>This feature can be used to display words commonly seen in a variety of geo-locations.<br> - adText is by default shown in the upper right corner of the top bar of the ad player.  <br> - However, if the Skip button is located in the top-right (via skipLocation), then the adText will be displayed in the upper left corner of the top bar. | A String of zero or more characters.<br>If the string is too long to fit in the space provided, the string will be truncated with the text "...".<br>If the string is empty, then no ad indicator will be displayed. | No | "Ad" | `adText : "publicité"` |
| `learnMore` | An optional button that, if enabled, is displayed next to the adText towards the outside.<br> - If adText is in the upper right corner, then the top bar will display Ad - Learn More in the upper right corner.<br> - If adText is in the upper left corner, then the top bar will display Learn More - Ad in the upper left corner.<br> - If enabled, the Learn More button will replace the video click behavior.  The user will need to click on the Learn More button to execute a click through. Clicking on the video then will NOT produce a click through. | JSON object which supports the following fields:<br><br> - `enabled` = boolean where <br>&nbsp; - `true`: Display the Learn More button.<br>&nbsp; - `false`: Do NOT display the Learn More button.<br>&nbsp; - Default value: `false`;<br><br> - `text` = (string) text to display in the Learn More position, if it is enabled.<br>&nbsp; - Default: `Learn More`.<br><br> - `separator` = (string) text to display in between the adText and Learn More text.<br>&nbsp; - Default value: `-`<br><br> - `clickToPause` = boolean indicating whether clicking on the button pauses the video.<br>&nbsp; - `true`: Clicking on button will pause/resume the video.<br>&nbsp; - `false`: Click on the button will have no effect on the playback of the video.<br>&nbsp; - Default value: `true` | No | {} | Sample Learn More button configuration<br>`learnMore: {`<br>  `enabled:  true`<br>`}` |
| `disableTopBar` | Specifies whether the top bar is visible during video playback. The top bar is used to display the Ad Indicator, SKIP button and any countdown text for skippability.<br>If it is not visible, then the skippability setting will be ignored. | Boolean<br> - `true`: The top bar will NOT be displayed during video playback.<br> - `false`: The top bar WILL be visible during video playback. | No | For Native Player: true<br><br>For all other players: false | `disableTopBar : true` |
| `controlBarPosition` | Indicates whether the position of the bottom control bar floats over the playback area or is fixed. | One of the following Strings:<br> - `"over"`: The bottom control bar will float over the playback area when the user interacts with the video; this is the default value for all platforms except Android and iOS.<br> - `"below"`: The bottom control bar will remain visible in a fixed position below the playback area during the duration of the ad; control bars on Android and iOS are always fixed below the playback area and this position cannot be altered.  | No | On desktop: "over"<br><br>On Android: "below"<br><br>On iOS:<br>"below" | `controlBarPosition : "below"`|
| `showMute` | Indicates whether to show the mute button on the player controls. | Boolean<br> - `true`: The Mute button will be displayed on the control bar.<br> - `false`: The Mute button will NOT be displayed on the control bar. | No | true | `showMute: false` |
| `showVolume` | Indicates whether to show the volume control on the player controls. | Boolean<br> - `true`: The Volume control will be displayed on the control bar.<br> - `false`: The Volume control will NOT be displayed on the control bar. | No | true | `showVolume: false` |
| `showProgressBar` | Specifies whether to show information about the video progress in the control bar. | You can either use a Boolean value or a String value:<br> - If the value = true, then the video countdown progress text will be displayed in the control bar.<br> - If the value = false, then no video progress will be displayed in the control bar.<br> - If the value is a string, it may be one of the following values:<br>&nbsp; - `text`: The video countdown text will be displayed in the control bar.<br>&nbsp; - `bar`: A graphical progress bar will be displayed at the top of the control bar; no text will be displayed.<br>&nbsp; - `both`: Both the video countdown text AND the graphical progress bar will be displayed in the control bar. | No | true | `showProgressBar : "bar"` |
| `allowFullscreen` | Specifies whether fullscreen support within the ad is supported.<br>If supported, goto and exit fullscreen buttons will appear on the player controls as indicated by the state of the ad. | Boolean<br> - `true`: goto and exit fullscreen buttons will be displayed in the control panel of the ad player.<br> - `false`: goto fullscreen button will NOT be displayed; users will not be able to play the ad in fullscreen. | No | true | `allowFullscreen : false` |
| `wrapperLimit` | Specifies the maximum number of XML redirects that are allowed to be considered when attempting to play an ad. | Integer<br>The number of XML documents being parsed in a wrapper chain to obtain the media file to play. This includes the number of wrapper XML documents and the inline XML.<br><br>If the number of steps in the XML chain equals or exceeds this limit, no ad will play. | No | 5 | `wrapperLimit : 5` |
| `companionContainers` | List of DIV ids for areas on the page that are available for companion ads. | Array<br>Contains list of DIV ids for DIV HTML elements that are present on the page. | No | undefined | `companionContainers : [`<br>  `"comp_ad_728" ,`<br>  `"comp_ad_300"`<br>`]` |
| `playerSkin` | Provides support to allow for custom skinning of the ad player skin. | JSON Object which may contain the following fields:<br> - `bigPlayButtonColor` - optional = string specifying CSS color value for the large click-to-play button; default value: `#3B4249`.<br><br> - `topBarColor` - optional = string specifying CSS color value of the background of the top bar in the player; default value: `black`.<br><br> - `topBarTextColor` - optional =string specifying CSS color value of the text in the top bar; default value: `#CCCCCC`.<br><br> - `controlBarHeight` - optional = integer specifying height of the bottom control bar in pixels; the size of the controls displayed in the control bar will adjust to accommodate the height of the control bar; default value: `30 px`.<br><br> - `controlBarColor` - optional = string specifying CSS color value for the background of the bottom control bar; default value: `#07141e`.<br><br> - `controlBarControlsColor` - optional =string specifying CSS color value of the text in the bottom control bar; default value: `#CCCCCC`.<br><br> - `progressBarElapsedColor` - optional = string specifying CSS color value of the bar that indicates the elapsed time of the video; default value = a blue with a diagonal pattern; note that when you change the color, the color will be solid.<br><br> - `volumeBarBackground` - optional = string specifying CSS color value of the filled-in portion of the volume bar; default value = a blue with a diagonal pattern; note that when you change the color, the color will be solid.<br><br> - `dividerColor` - optional = string specifying CSS color value of the divider line between the top bar and the playback area; default value: `#606060`.<br><br>**Note:** The CSS color values are expressed as a string and can be any color specifier that is acceptable to CSS: hex value, color name, RGB and RGBA values. | No | {} | `"playerSkin"   : {`<br> `"bigPlayButtonColor" :  "#3B4249" ,`<br> `"controlBarColor" :  "#000000" ,`<br>     `"controlBarControlsColor" :  "#CCCCCC" ,`<br> `"dividerColor" :  "#CCFFFF" ,`<br> `"topBarTextColor" :  "#CCCCCC" ,`<br>     `"topBarColor" :  "#000000" ,`<br> `"controlBarHeight"   : 40,`<br> `"progressBarElapsedColor"   :  "#FF0066" ,`<br> `"volumeBarBackground"   :  "#00CCA3"`<br>`}` |

## Notification Callback

The Notification Callback has the following prototype: function callback (event, data) where:

| Argument | Description | Acceptable Values | Required | Default |
|:---|:---|:---|:---|:---|
| `event` | Identifies the event about which status is being provided. | Event can be one of the following integers:<br> - `0`: Player failed to render ad<br>- `1`: Player has completed the ad playback<br>- `2`: Player ready to play the ad<br>- `3`: Player has ignored playing the ad based on configuration data<br>- `4`: Player has begun to render ad<br>- `5`: Player instance created<br> - `6`: Click-to-play status for an ad that was configured as a click-to-play placement<br><br>Some of the notifications will not be made for a simple VAST player; they are used in other products. | Yes | None |
| `data` | Provides additional information about the event being reported. | The value can be a String, a Javascript object, a player reference or undefined, depending on the event type being reported as follows:<br> - For event 0 – data = error data - this is a Javascript object which contains<br>&nbsp; - error = error code (integer)<br>&nbsp; - (optional) message = string describing the error<br><br> - For event 1 – no data is sent<br><br> - For event 2 – data = reference to player DIV element<br><br> - For event 3 – no data sent<br><br> - For event 4 – no data sent<br><br> - For event 5 – data = reference to player instance<br><br> - For event  6 – data = <br>&nbsp; - true if clicked or <br>&nbsp; - false if ready to click | No | Undefined |
