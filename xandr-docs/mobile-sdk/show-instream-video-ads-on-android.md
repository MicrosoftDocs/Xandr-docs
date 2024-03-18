---
title: Show Instream Video Ads on Android
description: This page describes how to use the SDK to fetch and display instream video ads in Android.
ms.custom: android-sdk
ms.date: 10/28/2023
---


# Show instream video ads on Android

This page describes how to use the SDK to fetch and display instream video ads.

> [!NOTE]
> **Maintain references to VideoAd objects**: It is your responsibility to keep a reference to the `VideoAd` object. It is not cached by the SDK.

## Step 1. Include the SDK in your project

If you use Maven, use the following Gradle config to install the version of the SDK with instream video support:

```
// Android: Gradle config to install the SDK and the Video SDK
repositories {
     mavenCentral()
}
dependencies {
     compile  'com.appnexus.opensdk:appnexus-instreamvideo:[8,9)'
}
```

<!-- If you prefer to download the source code, you [can get the latest release from Github](https://github.com/appnexus/mobile-sdk-android/releases/tag/8.9). -->

## Step 2: Cache the video Ad

To cache a video ad, set up a request object and supply it with either:

- A placement ID (as shown in the example below), or
- A combination of your Xandr member ID and an inventory code

Then register a `VideoAdLoadListener` which will signal whether the ad load succeeded or failed. This is optional but strongly recommended. If you don't set the `VideoAdLoadListener,` you can use the `VideoAd.isReady()` method to check whether the ad is available.

After that, call `VideoAd.loadAd()` to start caching the ad.

``` 
// Create a VideoAd instance
VideoAd videoAd = new VideoAd( this , "9924002" );
// Set the (optional) VideoAdLoadListener.
videoAd.setAdLoadListener( new VideoAdLoadListener() {
  @Override
   public void onAdLoaded(VideoAd videoAd) {
        Log.d(TAG,  "onAdLoaded" );
   }
   @Override
     public void onAdRequestFailed(VideoAd videoAd, ResultCode errorCode) {
        Log.d(TAG,  "onAdRequestFailed" );
     }
  });
// At this point you can set targeting parameters, the ad landing
// page, and many other options before calling `loadAd()`.  For
// details, see the SDK documentation.
// Load the VideoAd.
videoAd.loadAd();
```

## Step 3: Set up the video playback listener

Before showing the video ad, you'll need to set up the mandatory `VideoPlaybackListener`. The `onAdCompleted()` notification is required to show your content video after the ad finishes playing.

``` 
// Set the (mandatory) PlayBack Listener.
videoAd.setVideoPlaybackListener( new VideoAdPlaybackListener() {
   
@Override
public void onAdPlaying( final VideoAd videoAd) {
      Log.d(TAG,  "onAdPlaying::" );
   }
@Override
public void onQuartile(VideoAd view, Quartile quartile) {
Log.d(TAG,  "onQuartile::" + quartile);
}
//Resume your VideoPlayer with the 'onAddCompleted' notification.
@Override
public void onAdCompleted(VideoAd view, PlaybackCompletionState playbackState) {
Log.d(TAG,  "onAdCompleted::playbackState" + playbackState);
videoPlayer.start();
//The 'videoPlayer' here is your Application Content Video Player.
}
@Override
public void onAdMuted(VideoAd view,  boolean isMute) {
  Log.d(TAG,  "isAudioMute::" + isMute);
}
@Override
public void onAdClicked(VideoAd adView) {
Log.d(TAG,  "onAdClicked" );
   }           
@Override
public void onAdClicked(VideoAd videoAd, String clickUrl) {
Log.d(TAG,  "onAdClicked" );
   }
});
```

## Step 4: Pass activity lifecycle events to the Ad

Pass on the Activity Lifecycle callback events to VideoAd as shown below:

``` 
// This is important because it's used to resume the ad after an interruption by user activity.
@Override
public void onResume() {
     super .onResume();
     videoAd.activityOnResume();
}
@Override
public void onPause() {
     super .onPause();
     videoAd.activityOnPause();
}
// Used to clear the memory footprint of the VideoAd instance.
@Override
public void onDestroy() {
     super .onDestroy();
     videoAd.activityOnDestroy();
}
```

## Step 5: Show the video Ad

You are now all set to show the Video Ad by calling `playAd()` as shown below. Remember to pause your content video player before calling `VideoAd.playAd()`:

```
if (videoAd.isReady()) {
     // Pause your app's video player.
     videoPlayer.pause();
     // Play the Ad by passing the container. The container here is a
     // FrameLayout/RelativeLayout, on top of which the ad will be
     // displayed.
     videoAd.playAd(baseContainer);
}
```

## Pause and resume the video Ad

To pause or resume playing the video ad use the following method calls.

``` 
 public void resumeAd();
 public void pauseAd();
```

## Fetch the attributes of a loaded video creative

Once the video is loaded, you may retrieve various creative attributes:

``` 
public String getVastURL()  //Provide the VAST content URL
public int getVideoAdDuration()  //Provide the duration of the video
public String getVastXML()  //Provide the VAST content as an XML string
public String getCreativeURL()  //Provide the actual creative loaded
public VideoOrientation getVideoOrientation()  //Provide the Orientation of the Video rendered. Possible video orientations can be square, portrait, landscape or none
```

## Determine Ad play progress

You can determine how far the adPlay has progressed by retrieving the amount of time that has elapsed since the ad began playing:

``` 
public void getAdPlayElapsedTime(ResultCallback<String> resultCallback)
```

**Example**

See below for a complete working example of showing an instream video ad.

> [!NOTE]
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the VideoAd that is expected to be destroyed.

``` 
 package com.appnexus.example.simplevideo;
  
 import android.app.Activity;
 import android.net.Uri;
 import android.os.Bundle;
 import android.util.Log;
 import android.widget.RelativeLayout;
 import android.widget.VideoView;
  
 import com.appnexus.opensdk.ResultCode;
 import com.appnexus.opensdk.instreamvideo.Quartile;
 import com.appnexus.opensdk.instreamvideo.VideoAd;
 import com.appnexus.opensdk.instreamvideo.VideoAdLoadListener;
 import com.appnexus.opensdk.instreamvideo.VideoAdPlaybackListener;
  
  
 public class MainActivity extends Activity {
  
    public static final String TAG = MainActivity.class.getName();
  
    // The Ad Video instance.
    // Its important to create this as a Instance variable to make sure its not removed Garbage Collected.
    private VideoAd videoAd;
  
    // Content video player.
    private static VideoView videoPlayer;
  
    // Ad Container.
    private RelativeLayout baseContainer;
  
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        videoPlayer = (VideoView)findViewById(R.id.video_player);
        baseContainer = (RelativeLayout)findViewById(R.id.baseContainer);
        videoPlayer.setVideoURI(Uri.parse("https://acdn.adnxs.com/mobile/video_test/content/Xandr_HighRes.mp4"));
  
        // Initialize VideoAd
        videoAd =new VideoAd(this,"9924002");
  
        // Set the Ad-Load Listener
        videoAd.setAdLoadListener(new VideoAdLoadListener() {
                @Override
                public void onAdLoaded(VideoAd videoAd) {
                    // Pause App's Content Video Player
                    videoPlayer.pause();
                    // Play the VideoAd by passing the container.
                    videoAd.playAd(baseContainer);
                }
  
                @Override
                public void onAdRequestFailed(VideoAd videoAd, ResultCode errorCode) {
                    Log.d(TAG, "onAdRequestFailed::"+errorCode);
                    videoPlayer.start();
                }
            });
        // videoAd.setAge("25");
        // videoAd.setGender(AdView.GENDER.FEMALE);
        // videoAd.setLoadsInBackground(true);
        // videoAd.addCustomKeywords("KEY_1","VALUE_1");
        // videoAd.addCustomKeywords("KEY_2","VALUE_2");
        //Load the Ad.
        videoAd.loadAd();
        // Set PlayBack Listener.
        videoAd.setVideoPlaybackListener(new VideoAdPlaybackListener() {
                                @Override
                                public void onAdPlaying(VideoAd view){
                                        Log.d(TAG, "onAdPlaying");
                                }
                @Override
                public void onQuartile(VideoAd view, Quartile quartile) {
                    Log.d(TAG, "onQuartile::" + quartile);
                                           
                                        videoAd.getAdPlayElapsedTime(new ResultCallback<String>() {
                                        @Override
                                                public void onResult(String s) {
                                                        Log.d(TAG, "elapsed time::" + s);      
                                                }
                                        });
                }
  
                @Override
                public void onAdCompleted(VideoAd view, PlaybackCompletionState playbackState) {
                    Log.d(TAG, "onAdCompleted::playbackState" + playbackState);
                    videoPlayer.start();
                }
  
                @Override
                public void onAdMuted(VideoAd view, boolean isMute){
                    Log.d(TAG, "isAudioMute::"+isMute);
                }
  
                @Override
                public void onAdClicked(VideoAd adView) {
                    Log.d(TAG, "onAdClicked");
                }
 
                                @Override
                public void onAdClicked(VideoAd videoAd, String clickUrl) {
                        Log.d(TAG, "onAdClicked");
                }
            });
    }
  
 
    // Pass the Activity LifeCycle Callback's to VideoAd. This is very important for autoresuming the Video Ad after interruption.
    @Override
    public void onResume() {
        super.onResume();
        videoAd.activityOnResume();
    }
  
    @Override
    public void onPause() {
        super.onPause();
        videoAd.activityOnPause();
    }
  
    @Override
    public void onDestroy() {
        super.onDestroy();
        videoAd.activityOnDestroy();
    }
}
  
```
