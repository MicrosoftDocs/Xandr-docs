---
title: Outstream Video Player Options
description: Explore outstream video settings for Microsoft Monetize, configure in page code or on placement. Note that  AST overrides Monetize settings.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Outstream video player options

This topic describes settings available for configuring outstream video that can be configured in page code, or on the placement via Microsoft Monetize. Note that setting page code via Microsoft Advertising's seller tag (AST) overrides any settings created in Monetize.

## Page-level outstream options

> [!NOTE]
> The following Outstream options are set at the Publisher level, and are set under `rendererOptions` in the page code using [AST](../seller-tag/seller-tag.md). Options set this way will override any settings created in Monetize.

## General options

| Option | Values | Default | Description |
|--|--|--|--|
| **Video Player Setup** |  |  |  |
| `audioOnMouseover` (deprecated) | - true<br> - false<br> - integer | `true` | This setting is no longer supported or tested because of current browser limitations on sounds.<br>Play audio when the user's mouse is over the video, pause/unmute audio when the mouse is not over the video.<br>If an integer is specified, the audio will not start until that many milliseconds of continuous mouse hovering over the video. |
| `autoInitialSize` | true / false | `false` | If `true`, the player width will match the page container. If `false`, the player width set on the placement will be used. |
| `alignment` | center / left / right | `center` | Alignment of the player if its size is smaller than the container. |
| `playOnMouseover` | true / false | `false` | When this setting is `true`, while the user's mouse is over the video it will play. If the mouse leaves the video it will pause and resume playing when the mouse returns over the video.<br>When this setting is `false`, the video plays regardless of the user's mouse. |
| `playVideoVisibleThreshold` | 0-100 | `50` | The video will not start playing until the video container's visibility is above this threshold. If the video container's visibility drops below this threshold the video follows the behavior specified in `nonViewableBehavior`. |
| `nonViewableBehavior` | - "pause"<br> - "mute" | "`mute`" | - "pause"- Video will pause when below `playVideoViewableThreshold`, and resume playback when above `playVideoViewableThreshold`<br> - "mute" - Video will mute but not pause when below `playVideoViewableThreshold` and unmute when above `playVideoViewableThreshold`<br> &nbsp;&nbsp;  - When scrolled back above the viewable threshold, the video should not unmute if it has been muted or set to 0 volume explicitly by the user, we should simply restore the pervious volume state that existed when the user scrolled out of viewability. |
| `expandTime` | integer (milliseconds) | `1000` | The amount of time in milliseconds it takes to expand the ad and to collapse the ad. |
| `playerTechnology` | array of strings | [`"html5"`, `"flash"`] | VPAID media files with corresponding technology are given priority for display. Otherwise, other media files with their corresponding technology are displayed. |
| `aspectRatio` | - "auto"<br> - "16:9"<br>"4:3" | If not defined, and `fixedSizePlayer` is `false`, `16:9` | The aspect ratio of the video portion of the player. Does not take into account any control bars which do not overlay the video. "auto" uses the aspect ratio defined in the video metadata. |
| `maxHeight` | true / false / height in pixels | `false` | Optionally, enable and set a maximum height for the player as shown in the following example. The player will adjust to maintain the aspect ratio.<br><br> ``` "maxHeight": { "enabled": `true`, "height": 480 } ```<br><br>This setting was designed to optimize vertical video presentations and should only be used with a vertical aspect ratio. For more information, including recommended values, see [Vertical Video Formats](vertical-video-formats.md). |
| `fixedSizePlayer` | true / false | `false` | If `true`, final rendered player height will be the height of the entire player, including any top or bottom control bars.<br>If `false`, final rendered player height will be the height of the video area, and any extra control bars (top bar, bottom control bar) will increase the total height of the player. |

### Player's chrome settings

| Option | Values | Default | Description |
|--|--|--|--|
| `adText` | string | `Ad` | Ad indicator text shown in the top-right hand corner of the outstream ad unit.<br>If `skipLocation` is also top-right, the `skipText`, and subsequently `skipButtonText`, will be shown to the left of `adText` in the top-right corner (see skippable object below). |
| `disableCollapse` | true/false | `false` | If `true`, the outstream ad will not collapse at the end of the video. The last frame that was showing at the end of the video will show. No control bar, click to play button or countdown text will show. Ad Indicator and Skip button will remain. |
| `replay` | true / false | `false` | Enables a replay button on the card that plays the ad a second time when clicked. |
| `controlBarPosition` | string | `over` (except on Android) | Determines whether the position of the bottom control bar floats over the playback area or is fixed. Specify over to have the bottom control bar float `over` the playback area when the user interacts with the video Specify `below` to have the bottom control bar remain visible in a fixed position below the playback area during the duration of the ad. On Android, the control bar is always displayed in this position. |
| `showMute` | true / false | `true` | Show or hide the mute button in the control bar.<br>If `audioOnMouseOver` is set to `false`, a user activates sound by disabling the audio mute button. If `showMute` is also `false` and the audio mute button is hidden, a user activates sound by dragging the volume slider. |
| `showVolume` | true / false | `true` | Show or hide the volume slider on the control bar. |
| `showProgressBar` | true / false | `false` | Show or hide the progress bar on the control bar. |
| `allowFullscreen` | true / false | `true` | Show or hide the fullscreen button. |
| `disableTopBar` | true / false | `false` | If set to `true`, the top player chrome bar (with adText and `skipText`/`skipButtonText`) will not display. If set to `false` the top player chrome bar will display except in the following case - If empty text fields are specified, a chrome bar will still be displayed, but will be empty. |

## Disable collapse settings

These settings enable the user to control what actions will occur when
the video playback has completed.

| Option | Type | Default Value | Description |
|---|---|---|---|
| `enabled` | boolean or integer | `true` | If `true`, the outstream ad will not collapse at the end of the video and the last frame that was showing at the end of the video will be displayed. No control bar, click to play button or countdown text will display, and the Ad Indicator and Skip button will remain.<br>If `false`, the replay and hideControlBar values won't matter because the video will collapse on completion.<br>If an integer is passed, the player sets a delay in milliseconds equal to the passed integer before collapsing the ad. |
| `replay` | boolean | `false` | If `true`, a replay button displays once the video is completed, enabling the user to replay the video. |
| `hideControlBar` | boolean | `false` | If `true`, and the replay setting is `false`, the bottom control bar is hidden after video completion. |

## VPAID handler settings

These settings determine how the video player handles video documents that use VPAID.

> [!NOTE]
> When a VPAID ad reaches its final frame, the Outstream player hides the control bar, and does not display a replay button. This behavior prevents any potential conflicts with interactive end screen elements supplied by VPAID. The player handles all VPAID ads this way, regardless of the configuration specified in Monetize or in page-level Outstream settings.

| Option | Values | Default | Description |
|---|---|---|---|
| `vpaidTimeout` | integer (milliseconds) | `5000` | If a VPAID ad unit is showing, time to wait between a VPAID ad unit starting and when it actually starts before timing-out and collapsing the ad. We might encounter this if a VPAID ad unit attempts to run a secondary auction which is especially slow, or hits misconfigured servers. We will also likely encounter this in the case of a non-fully-compliant VPAID ad unit |
| `terminateUnresponsiveVPAIDCreative` | boolean | `false` | If a VPAID creative does not respond properly to a pause event, terminate it |
| `delayExpandUntilVPAIDInit` | true / false | `true` | If `true`, wait to expand video area for AdLoaded event to be returned and the correct position on the page before Outstream can be expanded in a VPAID case. If `false`, the outstream will expand as soon as it has a creative and is at the correct position on the page. |
| `delayExpandUntilVPAIDImpression` | true / false | `false` | Delay Outstream expansion for VPAID ads until `AdImpression` or `AdVideoStart` event has been received. Note that since we are starting the ad and delaying its visibility until Outstream expands, this might lead to a higher incidence of discrepancies in reporting. |

## Mobile setting

This setting enables the player on mobile devices.

| Option | Values | Default | Description |
|---|---|---|---|
| `enableInlineVideoForIos` | boolean | `true` | Enable inline video for iOS devices. |

## Not shown in UI settings

The following settings are for specialized configurations that aren't available through Microsoft Monetize.

| Option | Values | Default | Description |
|---|---|---|---|
| `parentIframeGeometryEvent` | string | n/a | For non-friendly iFrame implementation cases only. |
| `parentIframeGeometryCb` | function callback | n/a | For non-friendly iFrame implementation cases only. |
| `vpaidEnvironmentVars` | JSON Object | n/a | Sends JSON object containing vpaidEnvironmentVars to VPAID creative as "envinronmentVars" parameter of VPAID initAd() call. |
| `cbNotification` | function callback | n/a | Callback function to be called on specific ad unit. Function foodprint is: adCallback(eventType, eventName, adId, eventData) where eventType is one of VPAID, VAST, AdUnit and eventName will be in one of the following eventType categories:<br>**VPAID**: AdLoaded, AdStarted, AdStopped, AdSkipped, AdSkippableStateChange, AdSizeChange, AdLinearChange, AdDurationChange, AdExpandedChange, AdRemainingTimeChange, AdVolumeChange, AdImpression, AdVideoStart, AdVideoFirstQuartile, AdVideoMidpoint, AdVideoThirdQuartile, AdVideoComplete, onAdVClickThru, AdInteraction, AdUserAcceptInvitation, AdUserMinimize, AdUserClose, AdPaused, AdPlaying, AdLog, AdError<br>**VAST**: creativeView, start, midpoint, firstQuartile, thirdQuartile, complete, mute, unmute, pause, rewind, resume, fullscreen, expand, collapse, close, exitFullscreen, skip, progress, acceptInvitation, acceptInvitationLinear, closeLinear, impression, error<br>**AdUnit**: collapseStart, collapseEnd, expandStart, expandEnd, adComplete, renderedPlayerSize, waterfall (see eventData below)<br>adId will be the id for the ad which is defined by AST (target element ID) and passed to the renderer upon renderAd() call<br>eventData = additional data passed in with the event<br>For waterfall event, this will be an Object containing the following fields: status (stepStart, stepFail, stepSuccess, timeout), step, totalAvailableSteps, stepLimit, maxTime, timeRemaining, failureReason (if status = stepFail) |

## Waterfall handling settings with mediation

The following settings apply only when Video Mediation is configured.

With mediation, waterfall handling of video ads increases your likelihood of serving a viable creative within the timeout period. With the waterfall process, you can attempt to load a series of ads, stopping when a suitable ad is found. You can set the timeout period as well as the maximum number of mediation ad sources that will be checked when trying to find a suitable ad. Once you have enabled mediation on the placement via Monetize, you can set waterfall options to further fine-tune your timeout preferences.

| Option | Values | Default | Description |
|---|---|---|---|
| `waterfallTimeout` | integer | `15000` | Maximum amount of time in milliseconds that waterfall processing of mediated ad sources is allowed to run before it stops attempting to deliver a viable ad. |
| `waterfallSteps` | - 1 <br> - 0  <br> - positive integer | `-1` | Maximum number of waterfall attempts that are allowed to try and display the ad.<br>Mediation processing produces a list of ad sources to try to get a viable ad to render. This list may include mediated bids as well as an RTB ad (the ad that won the auction). The publisher (or renderer) can control the number of waterfall mediation ad sources to try in an attempt to show an ad.<br>The possible values for this option are interpreted as follows:<br> - `-1` = all the ad sources in the waterfall list will be processed until a viable ad is found or the waterfallTimeout has expired<br> - `0` = only one ad sources will be used to produce an ad - use the first ad on the list<br> - positive integer = the maximum number of non-rtb ad sources to try until a viable ad is found<br> &nbsp;&nbsp;&nbsp;- If the number of ad sources is less than the value of this property then all of the ad sources will be attempted<br> &nbsp;&nbsp;&nbsp; - If none of the non-rtb ad sources yields a viable ad source and the waterfall timeout has not expired, then the rtb ad should be attempted.<br> &nbsp;&nbsp;&nbsp; - If you anticipate that the number of attempts to render an ad will exceed 6, then it is recommended that you do set this value to some number greater than 6. |

## Player skinning settings

The following settings are nested under the `playerSkin` node, and determine the look and feel of the outstream player.

| Option | Values | Default | Description |
|---|---|---|---|
| `topBarColor` | string | "`black`" | Background color for the top chrome that contains ad indicator and skipping text<br>*the value of all player skin colors can be any css-ready string, including "`black`", "`#FFFFFF`", "`rgb(255,255,255)`" and "`rgba(255,255,255,1)`" |
| `topBarTextColor` | string | "`#CCCCCC`" | Text color for the top chrome that contains ad indicator and skipping text. |
| `dividerColor` | string | "`#555555`" | Color of the divider between the top chrome and the video. |
| `dividerHeight` | positive integer | `1` | Height of the divider between the top chrome and the video. |
| `controlBarColor` | string | "`#CCCCCC`" | Background color for the control bar that contains play button, elapsed time, and volume controls. |
| `bigPlayButtonColor` | string | "`#3B4249`" | Color of the play button that overlays the video when paused. |
| `controlBarControlsColor` | string | "`#CCCCCC`" | Control of the play button, elapsed time text, and volume controls in the control bar. |
| `controlBarDividerColor` | string | "`#555555`" | Color of the divider between the control bar and the video on iOS. Has no effect on desktop browser or android html5 player. |

## Sidestream settings

The following settings are configured using the `sidestream` node, and determine whether and how videos are played in sidestream mode.

| Option | Values | Default | Description |
|---|---|---|---|
| `enabled` | true / false | `false` | If `true`, sidestream behavior is enabled. |
| `startInSideStream` | true / false | `false` | When sidestream is enabled, setting this option to `true` specifies that the creative will begin playing in sidestream mode, instead of in the outstream player.<br>`startInSidestream=true` is not recommended for mediated placements.<br>**Warning**: Setting both `startInSidestream` and `returnToPage` to the same value can result in ad display problems and is not recommended. |
| `returnToPage` | true / false | `true` | When sidestream is enabled, setting this option to `true` specifies that when the user scrolls down after sidestream is initiated, the sidestream player closes and the ad pauses until the user scrolls up again, then resumes playing in the outstream player. Setting this option to "false" ensures that the video plays to completion in sidestream mode, and collapses the original outstream player.<br>**Warning**: Setting both startInSidestream and `returnToPage` to the same value can result in ad display problems and is not recommended. |
| `position` | "top-left"<br>"top-right"<br>"bottom-left"<br>"bottom-right" | "`bottom-right`" | Specifies corner of the publisher page which the player will move to when side-stream functionality is activated. |
| `xOffset` | integer | `0` | Specifies the distance from the page edge on the x-axis, in pixels which the player will be shown when side-stream functionality is activated. |
| `yOffset` | integer | `0` | Specifies the distance from the page edge on the y-axis, in pixels which the player will be shown when side-stream functionality is activated. |
| `width` | integer | `<blank>` | Specifies the width of the player in sidestream mode, if not set, the player will the the same width as it is in the non-sidestream mode. |
| `height` | integer | `<blank>` | Specifies the height of the player in sidestream mode, if not set, the player will the the same height as it is in the non-sidestream mode. |
| `maxPageOverlay` | integer |  | Specifies the maximum percentage of the browser window that sidestream will cover. If the size of the player will be larger than this percentage, the player will not go into sidestream mode, and will behave as described in the "nonViewablePlayer" option. |

## End card settings

The following settings are configured using the `endCard` node. They determine whether an end card is displayed when the player remains open after video play is complete. For an end card to be displayed, first tell the player not to collapse after play by setting `disableCollapse.enabled` to `true`. Otherwise, the player will close when the play is complete and the end card settings will be ignored.

| Option | Values | Default | Description |
|---|---|---|---|
| `enabled` | true / false | `false` | If `true`, an end card is displayed at the end of video play, while the video player remains open. However, if `disableCollapse.enabled` is set to `false`, the player will close and end card settings will be ignored. |
| `color` | string | `none` | When an end card is enabled, draws a colored layer on top of the final frame of the video. Use a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value). For example, enter `#000000` for black. |
| `clickable` | true / false | `true` | If set to `true`, the ad area remains clickable while the end card is shown. Clicking in the ad area opens the clickthrough URL from the ad that was just displayed, as if the ad had been clicked. |
| `imageURL` | Complete URL |  | The URL of the image (including https:) to be shown on the end card if no companion ad is specified or available. If you specify an image, an image layer is drawn on top of the color layer (if `color` is specified) or on top of the video frame.<br>The image is centered in the ad area and drawn at the native resolution of the source image unless you specify the size of the image using the `imageWidth` and `imageHeight` options.<br>**Note**: Typically, an end card image is used as the fallback, with a companion ad defined using companionID. The image is never displayed if a valid companion ad is available. |
| `imageWidth` | string | `none` | If `imageUrl` has been defined, the width of the rendered image. You can use an exact pixel width (e.g. "320px"), or specify a percentage-based width (e.g. "100%") so that the image scales when the ad area is resized. If imageWidth is not specified, the image is drawn at its native width. |
| `imageHeight` | string | `none` | If imageUrl has been defined, the height of the rendered image. You can use an exact pixel width (e.g. "200px"), or specify a percentage-based width (e.g. "100%") so that the image scales when the ad area is resized.<br>If image width is not specified, the image is drawn at its native width. |
| `showCompanion` | true / false | `true` | Specifies whether or not to show a companion ad (if available) on the end card. For ads that don't use companions, the image defined by imageUrl will be displayed on the end card.<br>For ads that contain multiple companions, the end card shows the companion ad that most closely matches the aspect ratio and size of the ad unit area. |

## Code sample

The following example shows a typical outstream video player setup.

```
rendererOptions: {
            "cbNotification": handlePublisherCb,
            "autoInitialSize": false,
            "alignment": "center",
            "playOnMouseover": false,
            "playVideoVisibleThreshold": 50,
            "expandTime": 1000,
            "adText": "Ad",
            "showMute": true,
            "showVolume": true,
            "showPlayToggle": true,
            "showBigPlayButton": true,
            "showProgressBar": false,
            "allowFullscreen": true,
            "vpaidTimeout": 5000,
            "terminateUnresponsiveVPAIDCreative": false,
            "vpaidEnvironmentVars": {},
            "enableInlineVideoForIos": true,
            "preloadInlineAudioForIos": false,
            "disableCollapse": {
                  "enabled": false,
                  "replay": false
              },
            "aspectRatio": "16:9",
            "nonViewableBehavior": "mute",
            "delayExpandUntilVPAIDInit": true,
            "delayExpandUntilVPAIDImpression": false,
            "delayStartUntilNotified": false,
            "controlBarPosition": "over",
            "disableTopBar": false,
            "waterfallTimeout": 15000,
            "waterfallSteps": -1,
            "skippable": {
                "enabled": true,
                "videoThreshold": 15,
                "videoOffset": 5,
                "skipLocation": "top-left",
                "skipText": "Video can be skipped in %%TIME%% seconds",
                "skipButtonText": "SKIP",
                "allowOverride": false
            },
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
            "fixedSizePlayer": false,
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
            "topMostViewableCheck": {
                "enabled": true,
                "checkVerticalOnly": true,
                "rateOfBeacons": 10
                },
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
            "endCard": {
                "enabled": true,
                "clickable": true,
                "color": "",
                "imageUrl": "",
                "imageWidth": "",
                "imageHeight": "",
                "showCompanion": true
               }
             }
```

## Placement-level outstream options

The options below can be set on the placement in Monetize or via the API.

> [!TIP]
> A best practice for setting up your inventory is to have a one-to-one mapping between an ad unit position on your website and a placement in Microsoft Advertising. In other words, try to have only one placement per ad unit position. With one-to-one mapping, you can control your outstream ad unit's appearance and behavior from the placement settings and provide any necessary additional configuration from the page.
>
> If you choose to map multiple ad unit positions to a single Run of Site placement, you control your outstream ad unit's appearance and behavior from the on-page settings. This decision allows you to use different settings for each ad unit position on your website.

| Monetize Field | API Field | Values | Default | Definition |
|---|---|---|---|---|
| `Skippable` | `supports_skippable` | true / false | `false` | If `true`, skippability is enabled. |
| `Player Width` | `width` | integer | `0` | The default width of the player. This field is mandatory.<br>If the width is zero, the autoInitialSize option will not automatically set the width of the player on the page. |
| `Playback Method` | `playback_method` | auto_play_sound_on/ <br>auto_play_sound_off/ <br>click_to_play/ <br>mouseover/auto_play_sound_unknown` | `null` | How the video is initiated and its audio options.<br>If the setting is null, the video will auto play and follow the `playOnMouseover` and `audioOnMouseover` settings. |
