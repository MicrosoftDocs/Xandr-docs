---
title : Set AAID usage for Android
description : The Google Advertising ID (AAID) for devices is an Android provided id to track the users for advertising purposes by the publishers who have an app on the Google Play Store (post getting consent from the users to do that). 
---


# Set AAID usage for Android

Here is an overview on Google Advertising ID (AAID).

## Overview

The Google Advertising ID (AAID) for devices is an Android provided id
to track the users for advertising purposes by the publishers who have
an app on the Google Play Store (post getting consent from the users to
do that). An API is introduced in Xandr mobile
SDK to enable or disable AAID usage by including or excluding
the AAID field in the ad request. By default, the value is set
as **false** for including the AAID field in the AdRequests.

| Property | Type | Attribute | Description |
|---|---|---|---|
| `isAAIDUsageDisabled` | boolean | read | To get current status of disableAAIDUsage. |
| `disableAAIDUsage` | boolean | write | To enable/disable the disableAAIDUsage. Default value is **false**. |

``` pre
   /**
    *  An AppNexus disableAAIDUsage is a boolean value, which exclude the AAID field in ad request.
    *  Default value of disableAAIDUsage is set to false
    */
   public static boolean isAAIDUsageDisabled()
   /**
    * Sets true to exclude the AAID field in ad request else false.
    * @param disable whether to disable AAIDUsage or not. default is false
    */
   public static void disableAAIDUsage(boolean disable)
```

## Example

``` pre
// To Set the disableAAIDUsage
SDKSettings.disableAAIDUsage(false);
// To Get the disableAAIDUsage status
SDKSettings.isAAIDUsageDisabled()
```
