---
Title : API for Exiting Banner Video from Fullscreen
Description : When a user presses the back button in an Android device after an
outstream video creative (banner ad view) is rendered and sent to full
screen mode, the activity with the placement is destroyed and the user
is routed to the previous activity in the Activity stack. To mitigate
ms.custom : android-sdk

---


# API for Exiting Banner Video from Fullscreen



When a user presses the back button in an Android device after an
outstream video creative (banner ad view) is rendered and sent to full
screen mode, the activity with the placement is destroyed and the user
is routed to the previous activity in the Activity stack. To mitigate
this kind of undesirable situation, Xandr Mobile
SDK provides an API, which on pressing of the back button, exits the
expanded video creative from full screen mode but keeps the user on the
same screen from where the video creative was originated instead of
navigating to a previous screen or an unrelated activity.



## Method

**exitFullscreenVideo**

This API is applicable only for Outstream Video (rendered using
BannerAdView) and ideally this is called from the activity's
`onBackPressed()`. This API should be used when the expanded video needs
to exit.

``` pre
/**
     * To be called by the developer when the expanded video needs to exit.
     * example: when activity's onBackPressed() function is called.
     */
    public boolean exitFullscreenVideo() {
        if (this.currentDisplayable != null && getAdResponseInfo().getAdType() == AdType.VIDEO) {
            return this.currentDisplayable.exitFullscreenVideo();
        }
        return false;
    }
```





## Example

``` pre
public boolean onBackPressed() {
        if (bav != null) {
            return bav.exitFullscreenVideo();
        }
        return false;
    }
```






