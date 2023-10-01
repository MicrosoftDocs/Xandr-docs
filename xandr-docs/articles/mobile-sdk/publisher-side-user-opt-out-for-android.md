---
Title : Publisher Side User Opt-Out for Android
Description : ## Overview
The publisher side user opt-out feature provides a new API call in
Mobile SDK which enables the publishers to set the information of 
users' choice of opt-in/out from tracking in the AdRequests. For any
---


# Publisher Side User Opt-Out for Android





## Overview

The publisher side user opt-out feature provides a new API call in
Mobile SDK which enables the publishers to set the information of 
users' choice of opt-in/out from tracking in the AdRequests. For any
AdRequest, Xandr Mobile SDK checks in the device
or OS environment level and populates the value for limitAdTracking
(LMT) in the background automatically (If LMT=true, it indicates that
the user opts out from tracking at the device or OS settings). However,
the publishers retain information about their users' opt-in/out of
tracking and thus required to pass that information if their user has
opted out to comply with their privacy regulations. To facilitate the
same, publisher side user opt-out feature is introduced in Mobile SDK.





## Methods 

**setDoNotTrack  
**

Setter method which enables the publisher side user opt-out feature.

``` pre
/**
 Do not track flag. Set this to true/false if you have information in the app about user opt-out.
 If set to true, tracking cookies and AAID will be disabled for all future auctions.
 Default value is false.
 */
public static void setDoNotTrack(boolean dnt) {
    Settings.getSettings().doNotTrack = dnt;
}
```

**getDoNotTrack**

Getter method which indicates whether the tracking is enabled or not. 

``` pre
/**
     * Returns true if Do not track is enabled.
     * False otherwise.
     */
    public static boolean getDoNotTrack() {
        return Settings.getSettings().doNotTrack;
    }
```





## Example

``` pre
//Setter
SDKSettings.setDoNotTrack(true);
//Getter
SDKSettings.getDoNotTrack();
```






