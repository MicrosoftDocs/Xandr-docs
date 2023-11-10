---
title: Background Threading on Android
description: In this article, learn about the Background Threading feature on Android and the methods supported.
ms.custom: android-sdk
ms.date : 10/28/2023
---

# Background threading on Android

> [!IMPORTANT]
> This offering is currently in Alpha and is subject to change.

> [!TIP]
> The Background Threading feature enables MobileSDK to execute the ad requests for different AdUnits like banner, interstitial, native, and videos as a background thread instead of a UI thread. This feature can be turned on or off by a method (`enableBackgroundThreading`). By default, Background Threading feature is disabled in MobileSDK which can be enabled by using this method.

## Methods

The following methods are supported.

### enableBackgroundThreading(boolean)

Method used to enable or disable the Background Threading feature flag, based on which the AdRequests will be executed on or off the background thread. By default, the boolean value for the method is set to false (which uses AsyncTask of Android). To enable the feature of background threading, the value needs to be set as true in the method.  
  
```
/**
 * This API can be used to process Ad request on the BGThread,
 * @param enable
 * true - For processing the AdRequest on BGThread
 * false - For processing the AdRequest using AsyncTask
 * default is set to false.
 * */
public static void enableBackgroundThreading(boolean enable)
```

### init()

Method that initializes the MobileSDK early in the apps lifecycle and executes the tasks that require UI thread during an AdRequest ahead of time. This method ensures that the MobileSDK will use background threading only during the execution of the actual AdRequest. To know about completion of the init method, a listener can be passed along with the method.

```
/**
* Should be called at the early lifecycle of the app.
* You can pass in a listener to listen to the completion of the init method.
* If you don't integrate with this API, you might fail to get the aaid, user agents for initial ad requests.
* This needs to be called on UI thread.
*/
public static void init(final Context context, final InitListener listener)
```

## Example

```
// enable the Background threading
SDKSettings.enableBackgroundThreading(true);
// call init before requesting the Ad
SDKSettings.init(context, new SDKSettings.InitListener() 
   {
     @Override public void onInitFinished() 
       {
         // Init has finished. 
       }
    }
  );
```
