---
title: User ID(s) Mapping on Android
description: Globalize Android ad requests with Xandr, send Publisher First party ID, and User IDs, set up once per app session, values persist within the session, not across sessions.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# User ID(s) mapping on Android

> [!NOTE]
> This offering is currently in Alpha and is subject to changes or deprecation without notice.

## Overview

Xandr offers you the option of sending **Publisher First party ID** and **User ID(s)** from third party sources in ad requests. They are global settings and it is sufficient to set the User ID(s) once per app session as these values would be used in all consecutive ad requests in the same session. Please note that, Xandr does not store these values across different app sessions.

## Mobile SDK structure

### Publisher first party ID

> [!NOTE]
> >**Deprecation Notice**:
> >
> > The **setExternalUid** and **getExternalUid** methods available in **NativeAdRequest**, **VideoAd, BannerAdView**, and **InterstitialAdView** classes are deprecated. You can use **setPublisherUserId** and **getPublisherUserId** described below in **SDKSettings** class instead. The deprecated methods will be removed in SDK v8.0.

You can set Publisher(First Party) User ID using the `setPublisherUserId` method in **SDKSettings** class in Mobile SDK API. The **getPublisherUserId** returns the value set which is the publisher user ID for the current application user.

```
/**
 * Specifies a string that corresponds to the Publisher(First Party) User ID for the current application user.
 * @param publisherUserId
 */
SDKSettings.setPublisherUserId(String publisherUserId);
 
/**
 * Returns the Publisher User Id for the current application user, initially added using {@link #setPublisherUserId(String)}
 * @@return publisherUserId as String.
 */
SDKSettings.getPublisherUserId();
```

### User ID

> [!NOTE]
> **Deprecation Notice**:
>
>The **setExternalUserIds** and **getExternalUserIds** methods available in **SDKSettings** class and **ANExternalUserIdSource** class are now deprecated and will be removed in SDK v8.0. You can use **setUserIds** and **getUserIds** methods in **SDKSettings** class and **ANUserId** class described below instead as a replacement.

Xandr supports User ID(s) from the below sources:

- Criteo
- The Trade Desk
- NetID
- LiveRamp  
- UID 2.0
- Publisher Provided Id / PPID (publishers can register their own source
  via API and can pass the user id)

You can set **User ID** by

- creating a List of **ANUserId** objects, and

- assigning the List  to the setUserIds() method in `ANSDKSettings.`

- The `getUserIds()`method returns the values set as a List for the
  current user.

```
     /**
       * A Map containing objects that hold External UserId parameters for the current application user.
       * @param userIdList
       */
      public static void setUserIds(List<ANUserId> userIdList){
          Settings.getSettings().userIds = userIdList;
      }
      /**
       * Returns the Map that hold External UserId parameters for the current application user, initially added using {@link #setExternalUserIds(Map<ANExternalUserIdSource,String>)}
       * @@return externalUserIds as Map.
       */
      public static List<ANUserId> getUserIds() {
          return Settings.getSettings().userIds;
      }
```

```
  // In ANUserId.java
  package com.appnexus.opensdk;
    
  public class ANUserId {
    
      public enum Source {
          CRITEO,
          THE_TRADE_DESK,
          NETID,
          LIVERAMP,
          UID2
      }
       
      public ANUserId(String source, String userId){};
    
      public ANUserId(ANUserId.Source source, String userId) {};
   
    
      public String getUserId() {
          return userId;
      }
    
      public String getSource() {
          return source;
      }
  }
```
  
## Examples

```
import android.app.Activity;
import android.content.Context;
import android.os.Bundle;
 
import com.appnexus.opensdk.ANExtendedUserIdSource;
import com.appnexus.opensdk.BannerAdView;
import com.appnexus.opensdk.SDKSettings;
 
import java.util.HashMap;
import java.util.Map;
 
public class MyActivity extends Activity {
 
    Context context;
    BannerAdView bav;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_my);
        context = this;
 
        List<ANUserId> userIds = new ArrayList<>();
        ANUserId tradeDeskUserID = new ANUserId(ANUserId.Source.THE_TRADE_DESK, "userid-ttd-foobar");
        userIds.add(tradeDeskUserID);
        ANUserId criteoUserId = new ANUserId(ANUserId.Source.CRITEO, "userid-Criteo-foobar");
        userIds.add(criteoUserId);
        ANUserId netIdUserID = new ANUserId(ANUserId.Source.NETID, "userid-netid-foobar");
        userIds.add(netIdUserID);
        ANUserId liveRampUserID = new ANUserId(ANUserId.Source.LIVERAMP, "userid-liveramp-foobar");
        userIds.add(liveRampUserID);
        ANUserId UID2UserId = new ANUserId(ANUserId.Source.UID2, "userid-uid2-foobar");
        userIds.add(UID2UserId);
        ANUserId genericUserID = new ANUserId("Generic Source", "userid-generic-foobar");
        userIds.add(genericUserID);
 
        SDKSettings.setUserIds(userIds);          // Set User Id from External Sources
 
        // Setting Publisher First Party Id
        SDKSettings.setPublisherUserId("PublisherUserId-foobar");
 
        // Load Banner Ad
        // Create the AdView and set its placement ID.  Tweak a few other settings.
        bav = new BannerAdView(context);
        bav.setPlacementID("Placement");
        bav.setAdSize(300, 50);
        bav.setAdListener(adListener);
 
        //If auto-refresh is enabled
        bav.loadAd();
    }
 
    @Override
    protected void onDestroy() {
        super.onDestroy();
    }
}
```
