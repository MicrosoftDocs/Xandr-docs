---
title: Show Banners on Android
description: This page has instructions and code samples for showing banner ads on Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Show banners on Android

This page has instructions and code samples for showing banner ads on Android.

You can configure your banner ad view using XML, Java, or a mixture of the two. The XML and Java equivalents are listed below.

- `opensdk:placement_id` or `adview.setPlacementID(String placementID)`: The placement ID associated with your app's inventory. You must include a placement ID or an error will be thrown. Example: `"123456"`.
  
  > [!NOTE]
  > Beginning with version RC2.8, you can also use an inventory code and member ID to request an ad (placement ID is still supported). Currently this is only available from Java (not XML). Note that if both inventory code and placement ID are passed in, the inventory code will be passed to the server instead of the placement ID.

  ```
  // Android: Java code that uses inventory code and member ID instead of placement ID (optional)
  adview.setInventoryCodeAndMemberID(int memberID, String inventoryCode)
  ```

- `opensdk:auto_refresh_interval` or `adview.setAutoRefreshInterval(long interval)`: The interval, in milliseconds, at which the ad view will request new
  ads, if autorefresh is enabled. The minimum period is 15 seconds. The default period is 30 seconds. Set this to 0 to disable autorefresh. Example: `"60000"`.
- `opensdk:ad_width` or `adview.setAdSize(int width, int height)`: The width of the advertisement to request from the server. If this is not set, the SDK requests an ad of at least `android:layout_width`. Note that the Java method `setAdSize` sets the width and height at the same time. Example: `"320"`.
- `opensdk:ad_height` or `adview.setAdSize(int width, int height)`: The height of the view. Note that the Java method `setAdSize` sets the width and height at the same time. Example: `"50dp"`.

If you're using XML, you must add the `xmlns:opensdk` namespace attribute describing your application to your layout tag; for example this might be a `RelativeLayout`, `LinearLayout`, or `FrameLayout`.

``` 
// Android: XML to configure the banner ad view (optional)
xmlns:opensdk="https://schemas.android.com/apk/res/com.example.SimpleBanner"
```

Here's how to declare a banner in XML. Note that you must replace *"YOUR PLACEMENT ID"* below with an active placement ID.

> [!NOTE]
> If you're using both XML and Java (`loadAd`) to define `BannerAdView`, define `auto_refresh_interval` in *either* XML or Java. Do not define `auto_refresh_interval` in both.

``` 
// Android: XML to declare banner ad view (optional)
<com.appnexus.opensdk.BannerAdView
    android:id="@+id/banner"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    opensdk:placement_id="YOUR PLACEMENT ID"
    opensdk:auto_refresh_interval="60000"
    opensdk:adWidth="320"
    opensdk:adHeight="50"
    opensdk:should_reload_on_resume="true"
    opensdk:opens_native_browser="true"
    android:expands_to_fit_screen_width="false"
    />
    
```

To show ads, you must set up a `BannerAdView`. The only required method is `setPlacementID`, but it's a good idea to set the ad size. Note that the height and width you specify here must match the size of the ad placement. The code below shows a banner ad (and assumes that your placement ID points at a 300x50 placement).

This simple example doesn't take advantage of all of the capabilities provided by the SDK - for example, you can also pass in the user's age and gender, as well as whether an ad click should open the device's native browser.

> [!NOTE]
> As best practices :
>
> - All SDK methods must be called on the main thread.
> - `activityOnDestroy()` must be called for the BannerAdView that is expected to be destroyed.

``` 
// Android: Java to show a banner ad
package com.example.simplebanner;
import android.os.Bundle;
import android.os.Handler;
import android.app.Activity;
import android.widget.FrameLayout;
import com.appnexus.opensdk.*;
import com.appnexus.opensdk.R.*;
public class MainActivity extends Activity {
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    // Create the AdView and set its placement ID.  Tweak a few other settings.
    final BannerAdView bav = new BannerAdView(this);
    bav.setPlacementID("1326299");
    bav.setAdSize(300, 50);
    bav.setAutoRefreshInterval(60000); // Set to 0 to disable auto-refresh
    bav.setShouldServePSAs(true);
    
    // Add the AdView to our layout 'n stuff.
    FrameLayout layout = (FrameLayout)findViewById(android.R.id.content);
    layout.addView(bav);
        bav.loadAd();
  }
@Override
protected void onDestroy() {
        if (bav != null) {
            bav.activityOnDestroy();
        }
        super.onDestroy();
    }
}
    
```
