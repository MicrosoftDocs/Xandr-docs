---
title: Get Facebook demand for native on Android
description: Learn how to use the Android SDK Facebook adapter to request, render, and track Facebook native ads.
ms.custom: android-sdk
ms.date: 09/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Get Facebook demand for native on Android

This article describes how to use the Android SDK Facebook adapter to retrieve and display native ads from Meta Audience Network.

## SDK installation

Add the Android SDK and Facebook CSR adapter to your app module's `build.gradle` file. The adapter version combines the Android SDK version and its supported Meta Audience Network version. For other releases, see [Android SDK release notes](android-sdk-release-notes.md).

```groovy
dependencies {
    implementation 'com.appnexus.opensdk:appnexus-sdk:9.12.0'
    implementation 'com.appnexus.opensdk.csr:appnexus-facebook-csr:9.12.0-6.22.0'
}
```

## Initialize Facebook's Audience Network SDK

Early in your app lifecycle, initialize Meta Audience Network.

### [Kotlin](#tab/kotlin1)

```kotlin
AudienceNetworkAds.buildInitSettings(this)
    .withInitListener {
        // Load ads after initialization completes
    }
    .initialize()
```

### [Java](#tab/java1)

```java
AudienceNetworkAds.buildInitSettings(this).withInitListener(new AudienceNetworkAds.InitListener() {
    @Override
    public void onInitialized(AudienceNetworkAds.InitResult initResult) {
        // Load ads after initialization completes
    }
}).initialize();
```

---

> [!NOTE]
> When you register the native ad, provide either a Meta `MediaView` or an Android `ImageView` for the icon. Choose the corresponding `FBNativeBannerAdResponse.registerView` overload.

## Create a native banner ad layout

In your activity layout, add a `com.facebook.ads.NativeAdLayout` container. This class wraps `FrameLayout` and enables Meta Audience Network to render its ad reporting flow.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    ...
    <com.facebook.ads.NativeAdLayout
        android:id="@+id/native_banner_ad_container"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true" />
    ...
</RelativeLayout>
```

[Click here to view a sample code](https://developers.facebook.com/docs/audience-network/guides/ad-formats/native-banner/android#layout) provided by Facebook for setting up native banner ad custom layouts.

## Create a native ad request and load the ad

> [!NOTE]
> Hold a reference to the request until you receive a response.

Check the response returned from `NativeAdRequest`. Register `FBNativeBannerAdResponse` directly with the Facebook adapter. Register other native responses with `NativeAdSDK`.

The following example assumes that `adView`, `nativeAdIconView`, and `nativeAdCallToAction` are initialized from your native ad layout.

### [Kotlin](#tab/kotlin2)

```kotlin
class MainActivity : AppCompatActivity(), NativeAdRequestListener, NativeAdEventListener {
    private lateinit var request: NativeAdRequest
    private var response: NativeAdResponse? = null
    private lateinit var adView: View
    private lateinit var nativeAdIconView: ImageView
    private lateinit var nativeAdCallToAction: Button

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        request = NativeAdRequest(this, "17823252") // Create the native ad request
        request.listener = this // Set the request listener
        request.loadAd() // Load the ad
    }

    override fun onAdLoaded(response: NativeAdResponse) {
        this.response = response
        nativeAdCallToAction.text = response.callToAction // Render the call-to-action text
        val clickableViews = listOf<View>(nativeAdCallToAction)

        if (response is FBNativeBannerAdResponse) {
            response.registerView(adView, nativeAdIconView, clickableViews, this) // Register the Facebook response
        } else {
            NativeAdSDK.registerTracking(response, adView, clickableViews, this) // Register other native responses
        }
    }

    override fun onAdFailed(errorCode: ResultCode, adResponseInfo: ANAdResponseInfo?) {
        Log.d("NativeBanner", "Failed: ${errorCode.message}")
    }

    override fun onAdWasClicked() = Unit
    override fun onAdWillLeaveApplication() = Unit
    override fun onAdWasClicked(clickUrl: String, fallbackURL: String) = Unit
    override fun onAdImpression() = Unit
    override fun onAdAboutToExpire() = Unit
    override fun onAdExpired() = Unit

    override fun onDestroy() {
        when (val currentResponse = response) {
            is FBNativeBannerAdResponse -> currentResponse.unregisterView() // Unregister the Facebook response
            null -> Unit
            else -> NativeAdSDK.unRegisterTracking(adView) // Unregister other native responses
        }
        response = null
        super.onDestroy()
    }
}
```

### [Java](#tab/java2)

```java
public class MainActivity extends AppCompatActivity
        implements NativeAdRequestListener, NativeAdEventListener {
    private NativeAdRequest request;
    private NativeAdResponse response;
    private View adView;
    private ImageView nativeAdIconView;
    private Button nativeAdCallToAction;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        request = new NativeAdRequest(this, "17823252"); // Create the native ad request
        request.setListener(this); // Set the request listener
        request.loadAd(); // Load the ad
    }

    @Override
    public void onAdLoaded(NativeAdResponse response) {
        this.response = response;
        nativeAdCallToAction.setText(response.getCallToAction()); // Render the call-to-action text
        List<View> clickableViews = Arrays.asList(nativeAdCallToAction);

        if (response instanceof FBNativeBannerAdResponse) {
            FBNativeBannerAdResponse facebookResponse = (FBNativeBannerAdResponse) response;
            facebookResponse.registerView(adView, nativeAdIconView, clickableViews, this); // Register the Facebook response
        } else {
            NativeAdSDK.registerTracking(response, adView, clickableViews, this); // Register other native responses
        }
    }

    @Override
    public void onAdFailed(ResultCode errorCode, ANAdResponseInfo adResponseInfo) {
        Log.d("NativeBanner", "Failed: " + errorCode.getMessage());
    }

    @Override public void onAdWasClicked() {}
    @Override public void onAdWillLeaveApplication() {}
    @Override public void onAdWasClicked(String clickUrl, String fallbackURL) {}
    @Override public void onAdImpression() {}
    @Override public void onAdAboutToExpire() {}
    @Override public void onAdExpired() {}

    @Override
    protected void onDestroy() {
        if (response instanceof FBNativeBannerAdResponse) {
            ((FBNativeBannerAdResponse) response).unregisterView(); // Unregister the Facebook response
        } else if (response != null) {
            NativeAdSDK.unRegisterTracking(adView); // Unregister other native responses
        }
        response = null;
        super.onDestroy();
    }
}
```

---

## Related

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Show Banner Native on Android](show-banner-native-on-android.md)
- [Show Native Ads on Android](show-native-ads-on-android.md)
