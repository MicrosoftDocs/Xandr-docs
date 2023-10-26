---
title: Add Targeting Parameters on Android
description: In this article, learn how to add targeting parameters for ads on Android.
ms.custom: android-sdk
---

# Add targeting parameters on Android

## User location

In this example, we get the user's location from Android and pass it along in the ad call:

```
import android.location.LocationManager;
import android.location.Location;

// Get the current location, and add it to the ad view.
LocationManager locationManager =
  (LocationManager) getApplicationContext().getSystemService(LOCATION_SERVICE);

Location location =
  locationManager.getLastKnownLocation(LocationManager.NETWORK_PROVIDER);

SDKSettings.setLocation(location);
    
```

This code assumes you provided the application location access by setting one or both of the `ACCESS_COARSE_LOCATION` and `ACCESS_FINE_LOCATION` permissions.

> [!NOTE]
> Developers should ensure adequate consent is obtained before sharing location information. Developers can control whether location is collected and sent by the SDK.

By default, the Android SDK automatically transmits location information if the Android Manifest allows location permissions to the app. If adequate permissions have not been obtained, or for any other reason, developers are able to instruct the SDK to not send the location. To disable the SDK from sending location, you can call:

```
com.appnexus.opensdk.utils.SDKSettings.setLocationEnabled(false);
    
```

> [!NOTE]
> This is a global setting for our mobile SDK only. Keep in mind that third Party SDKs will have their own settings.

## Age and gender

Advertisers may want to target ads by age and gender. In this example, we add the age and gender to an `AdView `.

```
// Set the user's age.  This can be a number, a year, or a
// numeric range such as "18-35".
adView.setAge("1978");

// Set the user's gender (if known).  This is used by
// advertisers for targeting.
adView.setGender(AdView.GENDER.MALE);
    
```
