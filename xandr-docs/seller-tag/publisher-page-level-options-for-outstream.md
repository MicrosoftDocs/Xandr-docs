---
title: Publisher Page-Level Options for Outstream
description: This page describes different settings available for configuring outstream video in page code. Some of the settings described in this page are Disable Collapse settings, End Card settings, Player Skinning settings, Sidestream settings to name a few.   
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---


# Publisher Page - Level options for outstream

This topic describes settings available for configuring outstream video in page code. These settings supplement the placement-level outstream parameters described in the main Monetize documentation.

> [!WARNING]
> Setting page code via Microsoft's seller tag (AST) overrides any settings created in Monetize.

The following outstream options are set at the publisher level, within the `rendererOptions` settings of the [Define Tag](define-tag.md). Options set through the API will override any settings created in Monetize.

## General options

| Option | Type | Default | Description |
|--|--|--|--|
| `alignment` | string | center | Alignment of the player if its size is smaller than the container. Accepted values are:<br>- center<br> - left<br> - right |  |
| `aspectRatio` | string | If not defined, and fixedSizePlayer is false, 16:9 | The aspect ratio of the video portion of the player. Does not take into account any control bars which do not overlay the video. The "auto" setting uses the aspect ratio defined in the video metadata. Accepted values are:<br>- "auto"<br>- "16:9"<br>- "4:3" |
| `audioOnMouseover (deprecated)` | - true<br>- false<br>- integer | true | This setting is no longer supported or tested because of current browser limitations on sounds.<br>Play audio when the user's mouse is over the video, pause/unmute audio when the mouse is not over the video.<br>If an integer is specified, the audio will not start until that many milliseconds of continuous mouse hovering over the video. |
| `autoInitialSize` | boolean | false | If true, the player width will match the page container. If false, the player width set on the placement will be used. |
| `cbNotification` |  |  | Callback function to be called on specific ad unit. Function footprint is:<br>```adCallback(eventType, eventName, adId, eventData)```<br>where eventType is one of VPAID, VAST, AdUnit and eventName will be in one of the following eventType categories: See [Table 1. Event Type Categories](#event-type-categories)<br><br>The `adId` value will be the id for the ad which is defined by AST (target element ID) and passed to the renderer upon `renderAd()` call.<br>The `eventData` value will be additional data passed in with the event.<br>For a waterfall event, this will be an object containing the following fields:<br>```status (stepStart, stepFail, stepSuccess, timeout), step, totalAvailableSteps, stepLimit, maxTime, timeRemaining, failureReason (if status = stepFail)``` |
| `disableCollapse` | object | n/a | Enables the user to control what actions will occur when the video playback has completed. See the Disable Collapse Settings table below for more details. |  |
| `endCard` | object | n/a | Configurations to determine whether an end card is displayed when the player remains open after video play is complete. See the End Card settings table below for detailed information. |  |
| `fixedSizePlayer` | boolean | false | If true, final rendered player height will be the height of the entire player, including any top or bottom control bars.<br>If false, final rendered player height will be the height of the video area, and any extra control bars (top bar, bottom control bar) will increase the total height of the player. |  |
| `learnMore` | object | n/a | If enabled a learnMore button is enabled  and clicking the video causes an ad-click and click-thru. See the Learn More Settings table below for more details. |  |
| `maxHeight` | true/false/height in pixels | false | Optionally, enable and set a maximum height for the player as shown in the following example. The player will adjust to maintain the aspect ratio.<br>`"maxHeight": { "enabled": true, "height": 480 }`<br>This setting was designed to optimize vertical video presentations and should only be used with a vertical aspect ratio. For more information, including recommended values, see  [Vertical Video Formats](../monetize/vertical-video-formats.md). |  |
| `parentIframeGeometryCb` | function callback | n/a | For non-friendly iFrame implementation cases only. |  |
| `parentIframeGeometryEvent` | string | n/a | For non-friendly iFrame implementation cases only. |  |
| `playerSkin` | object | n/a | Configurations to determine the look and feel of the outstream player. See the Player Skinning Settings table below for detailed information. |  |
| `playOnMouseover` | boolean | false | When this setting is true, while the user's mouse is over the video it will play. If the mouse leaves the video it will pause and resume playing when the mouse returns over the video.<br>When this setting is false, the video plays regardless of the user's mouse. |  |
| `playVideoVisibleThreshold` | integer | 50 | The video will not start playing until the video container's visibility is above this threshold. If the video container's visibility drops below this threshold the video follows the behavior specified in  nonViewableBehavior . Accepted range is 1-100. |  |
| `sidestream` | object | n/a | Configurations to determine whether and how videos are played in sidestream mode. See the Sidestream Settings table below for detailed information. |  |
| `skippable` | object | n/a | Configurations to determine if the video can be skipped and the skipping behavior. See the Skippable Settings table below for more details. |  |
| `vpaidEnvironmentVars` | JSON object | n/a | Sends JSON object containing vpaidEnvironmentVars to VPAID creative as "envinronmentVars" parameter of VPAID initAd() call. |  |
| `waterfallSteps` | integer | -1 | Maximum number of waterfall attempts that are allowed to try and display the ad. See the Waterfall Handling Settings with Mediation section below for more details. |  |
| `waterfallTimeout` | integer | 15000 | Maximum amount of time in milliseconds that waterfall processing of mediated ad sources is allowed to run before it stops attempting to deliver a viable ad. See the Waterfall Handling Settings with Mediation section below for more details. |  | 

### Event Type Categories

| Event Types | Fields |
|--|--|
| `AdUnit` | `collapseStart`, `collapseEnd`, `expandStart`, `expandEnd`, `adComplete`, `renderedPlayerSize`, `waterfall` |
| `VAST` | `creativeView`, `start`, `midpoint`, `firstQuartile`, `thirdQuartile`, `complete`, `mute`, `unmute`, `pause`, `rewind`, `resume`, `fullscreen`, `expand`, `collapse`, `close`, `exitFullscreen`, `skip`, `progress`, `acceptInvitation`, `acceptInvitationLinear`, `closeLinear`, `impression`, `error` |
| `VPAID` | `AdLoaded`, `AdStarted`, `AdStopped`, `AdSkipped`, `AdSkippableStateChange`, `AdSizeChange`, `AdLinearChange`, `AdDurationChange`, `AdExpandedChange`, `AdRemainingTimeChange`, `AdVolumeChange`, `AdImpression`, `AdVideoStart`, `AdVideoFirstQuartile`, `AdVideoMidpoint`, `AdVideoThirdQuartile`, `AdVideoComplete`, `onAdVClickThru`, `AdInteraction`, `AdUserAcceptInvitation`, `AdUserMinimize`, `AdUserClose`, `AdPaused`, `AdPlaying`, `AdLog`, `AdError` |

## Disable collapse settings

These settings enable the user to control what actions will occur when the video playback has completed.

| Option | Type | Default | Description |
|--|--|--|--|
| `enabled` | boolean or integer | true | If true, the outstream ad will not collapse at the end of the video and the last fame that was showing at the end of the video will be displayed. No control bar, click to play button or countdown text will display and the Ad Indicator and Skip button will remain.<br>If false, the replay and hideControlBar values won't matter because the video will collapse on completion.<br>If an integer is passed the player will set a delay in milliseconds equal to the passed integer before collapsing the ad. |
| `hideControlBar` | boolean | false | If true, and the replay setting is false, the bottom control bar will hide after video completion. |
| `replay` | boolean | false | If true, a replay button will show once the video is completed, enabling the user to replay the video. |

## End card settings

The following settings are configured using the `endCard` node. They determine whether an end card is displayed when the player remains open after video play is complete. For an end card to be displayed, first tell the player not to collapse after play by setting  `disableCollapse.enabled` to true. Otherwise, the player will
close when the play is complete and the end card settings will be ignored.

| Option | Type | Default | Description |
|--|--|--|--|
| `clickable` | boolean | true | If true , the ad area remains clickable while the end card is shown. Clicking in the ad area opens the clickthrough URL from the ad that was just displayed, as if the ad had been clicked. |
| `color` | string | n/a | When an end card is enabled, draws a colored layer on top of the final frame of the video. Use a  [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value) . For example, enter  #000000  for black. |
| `enabled` | boolean | false | If  true , an end card is displayed at the end of video play, while the video player remains open. However, if  disableCollapse.enabled  is set to  false , the player will close and end card settings will be ignored. |
| `imageHeight` | string | n/a | If `imageUrl` has been defined, the height of the rendered image. You can use an exact pixel width (e.g. "200px"), or specify a percentage-based width (e.g. "100%") so that the image scales when the ad area is resized.If `imageWidth` is not specified, the image is drawn at its native width. |
| `imageURL` | string | n/a | The URL of the image (including https:) to be shown on the end card if no companion ad is specified or available. If you specify an image, an image layer is drawn on top of the color layer (if  color  is specified) or on top of the video frame.The image is centered in the ad area and drawn at the native resolution of the source image unless you specify the size of the image using the `imageWidth` and `imageHeigh` options.<br>**Note**: Typically, an end card image is used as the fallback, with a companion ad defined using `companionID`. The image is never displayed if a valid companion ad is available. |
| `imageWidth` | string | n/a | If  `imageUrl`  has been defined, the width of the rendered image. You can use an exact pixel width (e.g. "320px"), or specify a percentage-based width (e.g. "100%") so that the image scales when the ad area is resized. If imageWidth is not specified, the image is drawn at its native width. |
| `showCompanion` | boolean | true | Specifies whether or not to show a companion ad (if available) on the end card. For ads that don't use companions, the image defined by `imageUrl` will be displayed on the end card. For ads that contain multiple companions, the end card shows the companion ad that most closely matches the aspect ratio and size of the ad unit area. |

## Learn more settings

> [!WARNING]
> The `learnMore` setting is only applicable for HTML5.

The learnMore setting enables the user to control if a **learnMore** button will be displayed when the outstream video is completed and what action will happen if a user clicks on the video during playback.

| Option | Type | Default | Description |
|--|--|--|--|
| `clickToPause` | boolean | true | If true, clicking on the video will pause the video. If false, clicking on the video will do nothing. |
| `enabled` | boolean | false | If true, **Learn More** button is enabled, and clicking the video area causes an ad-click and click-thru. |
| `separator` | string | "-" | The text of the separator between the **Learn More** text and the Ad Indicator. |
| `text` | string | "Learn More" | The text of the **Learn More** button. |

## Player skinning settings

Enables the configuring of the video player user interface.

| Option | Type | Default | Description |
|--|--|--|--|
| `bigPlayButtonColor` | string | "#3B4249" | Color of the play button that overlays the video when paused. |
| `controlBarColor` | string | "#CCCCCC" | Background color for the control bar that contains the play button, elapsed time, and volume controls. |
| `controlBarControlsColor` | string | "#CCCCCC" | Color of the play button, elapsed time text, and volume controls in the control bar. |
| `controlBarDividerColor` | string | "#555555" | Color of the divider between the control bar and the video on iOS. Has no effect on desktop browser or Android HTML5 player. |
| `dividerColor` | string | "#555555" | Color of the divider between the top chrome and the video. |
| `dividerHeight` | positive integer | 1 | Height of the divider between the top chrome and the video. |
| `topBarColor` | string | "black" | Background color for the top chrome that contains the ad indicator and skipping text. The value of all player skin colors can be any css-ready string, including `"black"`, `"#FFFFFF"`, `"rgb(255,255,255)"` and `"rgba(255,255,255,1)"`. |
| `topBarTextColor` | string | "#CCCCCC" | Text color for the top chrome that contains the ad indicator and skipping text. |

## Sidestream settings

If the outstream video is playing and the user scrolls the screen, if sidestream mode is enabled, the video player will reset to the corner of the screen indicated in the `position` option and continue playing the video. If no `position` is set the video player will reset to the bottom right of the screen.

| Option | Type | Default | Description |
|--|--|--|--|
| `enabled` | boolean | false | If true, sidestream behavior is enabled. |
| `height` | integer | n/a | Specifies the height of the player in sidestream mode. If not set, the player will the the same height as it is in the non-sidestream mode. |
| `maxPageOverlay` | integer | n/a | Specifies the maximum percentage of the browser window that sidestream will cover. If the size of the player will be larger than this percentage, the player will not go into sidestream mode, and will behave as described in the "nonViewablePlayer" option. |
| `position` | string | "bottom-right" | Specifies corner of the publisher page which the player will move to when side-stream functionality is activated.<br>Options are:<br>- "top-left"<br>-"top-right"<br>- "bottom-left"<br>- "bottom-right" |
| `returnToPage` | boolean | true | When sidestream is enabled, setting this option to  true  specifies that when the user scrolls down after sidestream is initiated, the sidestream player closes and the ad pauses until the user scrolls up again, then resumes playing in the outstream player. Setting this option to "false" ensures that the video plays to completion in sidestream mode, and collapses the original outstream player.<br>**Warning**: Setting both  startInSidestream  and  returnToPage  to the same value can result in ad display problems and is not recommended. |
| `startInSideStream` | boolean | false | When sidestream is enabled, setting this option to  true  specifies that the creative will begin playing in sidestream mode, instead of in the outstream player.<br>`startInSidestream=true` is not recommended for mediated placements.<br>**Warning**: Setting both  startInSidestream  and  returnToPage  to the same value can result in ad display problems and is not recommended. |
| `width` | integer | n/a | Specifies the width of the player in sidestream mode. If not set, the player will the the same width as it is in the non-sidestream mode. |
| `xOffset` | integer | 0 | Specifies the distance from the page edge on the x-axis, in pixels which the player will be shown when side-stream functionality is activated. |
| `yOffset` | integer | 0 | Specifies the distance from the page edge on the y-axis, in pixels which the player will be shown when side-stream functionality is activated. |

## Skippable settings

These settings determine if the user can skip the content playing in the video player and how the skip behavior will function.

| Option | Type | Default | Description |
|--|--|--|--|
| `allowOverride` | boolean | false | If set to `true`, any skip offset from a VAST 3.0 skipoffset setting will take precedence over the publisher settings, in full compliance with the [VAST 3.0 spec](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf). <br><br>**Note**: In this case if set to `true`, and no `skipoffset` is defined in the Ad XML, no skip button will be shown. |
| `enabled` | boolean | true | Override of `skippable` options, if set to `false`, skip option will not show. |
| `skipButtonText` | string | "SKIP" | Text displayed for the skip button. When the button is clicked the outstream ad unit is collapsed. |
| `skipLocation` | string | "top-left" | Location of the `skipText` and `skipButtonText`. Options are `top-left` and `top-right`.<br>If set to top-left, the `skipText`, and subsequently `skipButtonText`, will be displayed on the top left corner of the player while the adText will be displayed on the top right corner.<br>If set to top-right, the `skipText`, and subsequently `skipButtonText`, will be displayed on the top right corner of the player while the adText will be displayed on the top left corner. |
| `skipText` | string | "Video can be skipped in %%TIME%% seconds" | Text displayed to notify the user of when skippability will be available. Use %%TIME%% to insert the remaining time. |
| `videoOffset` | integer | 5 | Time, in seconds, after which the video will be skippable, if enabled and the video's duration is greater than `videoThreshold`. |
| `videoThreshold` | integer |  | Video must be longer than this length (in seconds) for the `skippable` option to be enabled.<br>**Note**: that video length is rounded to the closest second. For example: video lengths of 14.97 and 15.23 seconds will be treated as 15 second videos. |

## Waterfall handling settings with mediation

> [!WARNING]
> The following settings apply only when Video Mediation is configured.

With mediation, waterfall handling of video ads increases your likelihood of serving a viable creative within the timeout period. With the waterfall process, you can attempt to load a series of ads, stopping when a suitable ad is found. You can set the timeout period as well as the maximum number of mediation ad sources that will be checked when trying to find a suitable ad. Once you have enabled mediation on the placement via Monetize, you can set waterfall options to further fine-tune your timeout preferences.

## Waterfall step

Setting waterfallSteps (defineTag.rendererOptions.waterfallsteps) enables the mediation process to produce a list of ad sources from which to get a viable ad to render. This list may include mediated bids as well as an RTB ad (the ad that won the auction). The publisher (or renderer) can control the number of waterfall mediation ad sources to try in an attempt to show an ad.

The possible values for this option are interpreted as follows:

- -1 = all the ad sources in the waterfall list will be processed until a viable ad is found or the waterfallTimeout has expired.
- 0 = only one ad sources will be used to produce an ad - use the first ad on the list.
- positive integer = the maximum number of non-rtb ad sources to try until a viable ad is found.
  - If the number of ad sources is less than the value of this property then all of the ad sources will be attempted
  - If none of the non-rtb ad sources yields a viable ad source and the waterfall timeout has not expired, then the rtb ad should be attempted.
  - If you anticipate that the number of attempts to render an ad will exceed 6, then it is recommended that you do set this value to some number greater than 6. The default value is -1.

## Player's chrome setting

| Option | Type | Default | Description |
|--|--|--|--|
| `adText` | string | Ad | Ad indicator text shown in the top-right hand corner of the outstream ad unit.<br>If `skipLocation` is also top-right, the skipText, and subsequently `skipButtonText`, will be shown to the left of adText in the top-right corner (see skippable object below). |
| `allowFullscreen` | boolean | true | Show or hide the fullscreen button. |
| `controlBarPosition` | string | over (except on Android) | Determines whether the position of the bottom control bar floats over the playback area or is fixed. Specify  over  to have the bottom control bar float over the playback area when the user interacts with the video Specify  below  to have the bottom control bar remain visible in a fixed position below the playback area during the duration of the ad. On Android, the control bar is always displayed in this position. |
| `disableCollapse` | boolean | false | If true, the outstream ad will not collapse at the end of the video. The last frame that was showing at the end of the video will show. No control bar, click to play button or countdown text will show. Ad Indicator and Skip button will remain. |
| `disableTopBar` | boolean | false | If set to  true , the top player chrome bar (with adText and skipText/skipButtonText) will not display. If set to  false  the top player chrome bar will display except in the following case - If empty text fields are specified, a chrome bar will still be displayed, but will be empty. |
| `showMute` | boolean | true | Show or hide the mute button in the control bar.<br>If `audioOnMouseOver` is set to false, a user activates sound by disabling the audio mute button. If `showMute` is also false and the audio mute button is hidden, a user activates sound by dragging the volume slider. |
| `showProgressBar` | boolean | false | Show or hide the progress bar on the control bar. |
| `showVolume` | boolean | false | Show or hide the volume slider on the control bar. |  | 

### VPAID handler settings

These settings determine how the video player handles video documents that use VPAID.

> [!NOTE]
> When a VPAID ad reaches its final frame, the Outstream player hides the control bar, and does not display a replay button. This behavior prevents any potential conflicts with interactive end screen elements supplied by VPAID. The player handles all VPAID ads this way, regardless of the configuration specified in  or in page-level Outstream settings.

| Option | Type | Default | Description |
|--|--|--|--|
| `delayExpandUntilVPAIDInit` | boolean | true | If true, wait to expand video area for AdLoaded event to be returned and the correct position on the page before Outstream can be expanded in a VPAID case. If false, the outstream will expand as soon as it has a creative and is at the correct position on the page. |
| `delayExpandUntilVPAIDImpression` | boolean | false | Delay Outstream expansion for VPAID ads until  AdImpression  or  AdVideoStart  event has been received. Note that since we are starting the ad and delaying its visibility until Outstream expands, this might lead to a higher incidence of discrepancies in reporting. |
| `terminateUnresponsiveVPAIDCreative` | boolean | false |  |
| `vpaidTimeout` | integer (milliseconds) | 5000 | If a VPAID ad unit is showing, time to wait between a VPAID ad unit starting and when it actually starts before timing-out and collapsing the ad. We might encounter this if a VPAID ad unit attempts to run a secondary auction which is especially slow, or hits misconfigured servers. We will also likely encounter this in the case of a non-fully-compliant VPAID ad unit. |

### Mobile settings

This setting enables the player on mobile devices.

| Option | Type | Default | Description |
|--|--|--|--|
| `enableInlineVideoForIos` | boolean | true | Enable inline video for iOS devices. |

### AMP settings

Outstream works in AMP by inserting itself into the existing banner code for the AMP-AD tag, when the type=appnexus.  We also recommend follows the guidelines called out in the [AMP-IFRAME](https://amp.dev/documentation/components/amp-iframe)behavior section of the AMP developer documentation.

## Restricted/Limited Options for AMP

If AST detects it is running under an AMP page, it will override and/or turn off the following settings:

The following settings are either not available on AMP pages or have restricted or limited values available to them:

| Option | Type | Default | Description |
|--|--|--|--|
| `alignment` | string | "center" | Not supported on AMP pages. |
| `audioOnMouseover` | boolean | false | Not applicable for mobile devices. |
| `autoInitialSize` | boolean | false | Not supported on AMP pages. The player size can be changed only thru {"sizes" : [300,250]} in the publisher's options page. |
| `controlBarPosition` | string | "over" | On AMP pages, the control bar always acts like "below", and is not configurable. |
| `expandTime` | integer | 0 | Not supported on AMP pages. If AST detects it is running under an AMP page, it will override the passed in setting and set to the default. |
| `playOnMouseover` | boolean | false | Not applicable for mobile devices. |
| **Mobile** |  |  |  |
| `enableInlineVideoForIos` | boolean | true | Not supported on AMP pages. |
| **Side Stream Node** |  |  |  |
| `enabled` | boolean | false | Not supported on AMP pages. All other side stream settings are |
| **Disable Collapse** |  |  |  |
| `hideControlBar` | boolean | false | Not supported on AMP pages. |

## Code sample

``` 
rendererOptions: {
                        "adText": "Ad",
            "alignment": "center",
                        "allowFullscreen": true,
                        "aspectRatio": "16:9",
                        "autoInitialSize": false,
                        "cbNotification": handlePublisherCb,
                        "controlBarPosition": "over",
                        "delayExpandUntilVPAIDInit": true,
            "delayExpandUntilVPAIDImpression": false,
            "delayStartUntilNotified": false,
                        "disableCollapse": {
                  "enabled": false,
                  "replay": false
              },
                        "disableTopBar": false,
                        "enableInlineVideoForIos": true,
                        "endCard": {
                "enabled": true,
                "clickable": true,
                "color": "",
                "imageUrl": "",
                "imageWidth": "",
                "imageHeight": "",
                "showCompanion": true
               },
            "expandTime": 1000,
                        "fixedSizePlayer": false,
                        "intervals": {
                "playAndPause": 250,
                "focusAndBlur": 500
                },
            "learnMore": {
                "enabled": false,
                "separator": "-",
                "text": "Learn More",
                "clickToPause": true
                },
                        "maxHeight": {
                        "enabled": true,
                        "height": 480
                        }
            "nonViewableBehavior": "mute",
            "playOnMouseover": false,
            "playVideoVisibleThreshold": 50,
                        "playerSkin": {
                "topBarColor": "#5A1011",
                "topBarTextColor": "yellow",
                "dividerColor": "lightblue",
                "dividerHeight": 1,
                "controlBarColor": "blue",
                "bigPlayButtonColor": "red",
                "controlBarControlsColor": "yellow",
                    "controlBarDividerColor": "red",
                    "videoBackgroundColor": ""
                },
            "preloadInlineAudioForIos": false,
            "showMute": true,
            "showVolume": true,
            "showPlayToggle": true,
            "showBigPlayButton": true,
            "showProgressBar": false,
                        "sideStream": {
                "enabled": true,
                "startInSideStream": false,
                "returnToPage": true,
                "position": "top-right",
                    "xOffset": 0,
                    "yOffset": 0,
                    "maxPageOverlay": 50,
                    "width": 300,
                    "height": 250,
                },
                        "skippable": {
                "enabled": true,
                "videoThreshold": 15,
                "videoOffset": 5,
                "skipLocation": "top-left",
                "skipText": "Video can be skipped in %%TIME%% seconds",
                "skipButtonText": "SKIP",
                "allowOverride": false
            },
            "terminateUnresponsiveVPAIDCreative": false,
                        "topMostViewableCheck": {
                "enabled": true,
                "checkVerticalOnly": true,
                "rateOfBeacons": 10
                },
            "vpaidTimeout": 5000,
            "vpaidEnvironmentVars": {},
            "waterfallTimeout": 15000,
            "waterfallSteps": -1
        }
```
