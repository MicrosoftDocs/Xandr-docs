---
title: Show Instream Video Ads on iOS
description: This page is a step-by-step guide to show instream ads. The steps include to Initialize the video ad Object, Load the video ad, Show the video ad and few others which are explained in this page.   
ms.custom: ios-sdk
ms.date: 10/28/2023

---


# Show instream video ads on iOS

This page describes how to use the SDK to fetch and display instream video ads.

## Prerequisite

Include the SDK in your project. As of the [version 3.0 release](https://github.com/appnexus/mobile-sdk-ios/releases/tag/3.0), the SDK has instream video support. For instructions on how to integrate the SDK, see [Integrate the SDK](ios-sdk-integration-instructions.md).

## Steps to show instream ads

### Step 1: Initialize the video ad Object

A video ad can be fetched and displayed with as few as three methods `initWithPlacementId:`, `loadAdWithDelegate:` and `playAdWithContainer:withDelegate:`.
Defining the delegates for loading and playback will provide granular feedback for the video ad lifecycle.

In this step, initialize `ANInstreamVideoAd` with the placement ID.

``` 
ANInstreamVideoAd  *videoAd  = [[ANInstreamVideoAd alloc] initWithPlacementId:@"MY-PLACEMENT-ID"];
```

### Step 2: Load the video ad

Load the video ad and (optionally) define the `ANInstreamVideoAdLoadDelegate`.

Using the `ANInstreamVideoAdLoadDelegate` is highly recommended. It indicates when the load is complete or, alternatively, whether an error occurred during load.

The delegates return the instance of `ANInstreamVideoAd`, expressed as a reference to its superclass `ANAdProtocol`. It is shared with other Mobile SDK ad formats. The video ad object retains state that may be useful to refer during the lifecycle of the video ad.

Video ad state includes the placement ID, whether the video ad was clicked or skipped, and error feedback in the case of failure. (For complete details, see *`ANInstreamVideoAd.h`* .)

``` 
@interface  ViewController()  <ANInstreamVideoAdLoadDelegate, ANInstreamVideoAdPlayDelegate>
    //...
@end
@protocol  ANInstreamVideoAdLoadDelegate <NSObject>
    @required
    - (void) adDidReceiveAd:(id<ANAdProtocol>)ad;
    @optional
    - (void) ad:(id<ANAdProtocol>)ad requestFailedWithError:(NSError *)error;
@end
[videoAd loadAdWithDelegate:self];
```

## Step 3: Show the video ad

Display the video ad over your content container `UIView` and define the `ANInstreamVideoAdPlayDelegate`.

The delegate methods return the instance of `ANInstreamVideoAd`, expressed as a reference to its superclass `ANAdProtocol`. It is shared with other Mobile SDK ad formats. In addition to returning video ad state, the required method `adDidComplete:withState:` indicates when the video ad has completed.

``` 
@protocol  ANInstreamVideoAdPlayDelegate <NSObject>
    @required
    - (void) adDidComplete:  (id<ANAdProtocol>)ad
                 withState:  (ANInstreamVideoPlaybackStateType)state;
    @optional
    - (void) adCompletedFirstQuartile:  (id<ANAdProtocol>)ad;
    - (void) adCompletedMidQuartile:    (id<ANAdProtocol>)ad;
    - (void) adCompletedThirdQuartile:  (id<ANAdProtocol>)ad;
        - (void) adPlayStarted: (id<ANAdProtocol>)ad;
         //...
@end
[videoAd playAdWithContainer:MY-VIDEO-CONTENT-UIVIEW withDelegate:self];
```

`ANInstreamVideoAdPlayDelegate` contains many useful optional methods that further define video ad playback state and lifecycle for both the video ad and the landing page. (See *`ANInstreamVideoAd.h`* for complete details.)

## Pause and resume the video ad

To pause or resume playing the video ad use the following method calls:

``` 
(void) pauseAd;
 
 (void) resumeAd; 
```

## Choose which browser opens the landing page

When the video ad is clicked, video ad playback is paused and the click tracker is fired. Then, the click-through URL is opened in the in-app browser OR in the native browser according to the setting of the `opensInNativeBrower` property:

- *In-app Browser*: Click-through content loads within the app in a pop-up `UIView`.
- *Native Browser*: The app is suspended so the click-through content may load in the native browser.

The following properties are exposed by `ANInstreamVideoAd` to manage the target browser and whether the landing page loads before or after the landing page is displayed.

``` 
videoAd.opensInNativeBrowser = NO;           // DEFAULT is NO.
videoAd.landingPageLoadsInBackground = YES;  // DEFAULT is YES.
```

When the user returns from the browser, the video ad will resume playback.

## Load more than one video ad per session

Any number of video ads may be loaded in a single session. Accomplish this by calling `initWithPlacementId:` and `loadAdWtihDelegate:` once for each video ad object.

## Fetch the attributes of a loaded video creative

Once the video is loaded, you may retrieve various attributes of the creative:

``` 
-(NSUInteger) getAdDuration; //Provide the duration of the loaded video
-(NSString *) getCreativeURL; //Provide the creative that will be played
-(NSString *) getVastURL; //Provide the vastURL that is loaded
-(NSString *) getVastXML: //Provide the vastXML that is loaded
-(ANVideoOrientation) getVideoOrientation; //Provide the Orientation of the Video rendered. Possible video orientations can be square, portrait, landscape or none
```

## Determine ad play progress

You can determine how far the adPlay has progressed.

``` 
-(NSUInteger) getAdPlayElapsedTime;
```

## Video ad fullscreen display

Mobile SDK provides no functionality for displaying video ads or developer designated content in full screen mode. The video ad container automatically appears over the frame of the content container view using the same dimensions and positioning of the content container view. (See above `playWithAdContainer:withDelegate:`.)

This means you have control over whether the video ad displays in full screen mode by managing the frame of the content container view. By extension, if you want to give control over full screen mode to the user, you must provide appropriate interface options to the user.

> [!NOTE]
> Video Playback Controls
>
> In iOS, it is idiomatic to use the transport controls provided by `AVPlayerViewController` with property `showsPlaybackControls`. This method is incompatible with Xandr's Mobile SDK because, in this case, the full screen option creates a modal view which displays over all current views, obscuring the video ad container which displays over the content container. Full screen functionality for the video ad must be handled some means other than creating a modal view.
