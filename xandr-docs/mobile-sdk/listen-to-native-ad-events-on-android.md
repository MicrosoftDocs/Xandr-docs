---
title: Listen to native ad events on Android
description: Learn how to use NativeAdEventListener to receive impression, click, navigation, and expiration events on Android.
ms.custom: android-sdk
ms.date: 09/18/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Listen to native ad events on Android

This article describes how to use `NativeAdEventListener` to receive events for native ads.

## Overview

`NativeAdEventListener` notifies your app about native ad impressions, clicks, navigation away from the app, and expiration. After rendering the native ad assets, pass a `NativeAdEventListener` to the selected `NativeAdSDK.registerTracking()` overload. This registers the container for tracking and associates the listener with the response. For registration options, see [Show native ads on Android](show-native-ads-on-android.md#register-tracking).

Unregister the container before reusing it for another response or when it is no longer displayed.

## Methods

Use the following methods on `NativeAdEventListener`:

| Method | Description |
|:---|:---|
| `void onAdWasClicked()` | Called after a native ad click when `clickThroughAction` is `OPEN_SDK_BROWSER` or `OPEN_DEVICE_BROWSER`. The SDK opens the click-through destination. |
| `void onAdWasClicked(String clickUrl, String fallbackURL)` | Called after a native ad click when `clickThroughAction` is `RETURN_URL`. Your app is responsible for handling the returned click-through URL or fallback URL. |
| `void onAdWillLeaveApplication()` | Called before the click-through action moves the user from your app to another app, such as the device browser. |
| `void onAdImpression()` | Called after the SDK records the native ad impression and fires its impression trackers. |
| `void onAdAboutToExpire()` | Called shortly before the native ad response expires, allowing your app to prepare a replacement ad. |
| `void onAdExpired()` | Called when the native ad response expires and can no longer be registered for tracking. |

## Example

### [Kotlin](#tab/kotlin1)

```kotlin
class NativeAdActivity : AppCompatActivity(), NativeAdRequestListener, NativeAdEventListener {
    private lateinit var nativeAdRequest: NativeAdRequest
    private lateinit var nativeContainer: View
    private var nativeAdResponse: NativeAdResponse? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_native)

        nativeContainer = findViewById(R.id.native_ad_container)
        nativeAdRequest = NativeAdRequest(this, "123456") // Create a request for the placement ID
        nativeAdRequest.listener = this // Set the request listener
        nativeAdRequest.loadAd() // Load the ad
    }

    override fun onAdLoaded(response: NativeAdResponse) {
        nativeAdResponse = response
        findViewById<TextView>(R.id.native_ad_title).text = response.title // Render the native ad title
        NativeAdSDK.registerTracking(response, nativeContainer, this) // Register tracking and event callbacks
    }

    override fun onAdFailed(errorCode: ResultCode, adResponseInfo: ANAdResponseInfo?) {
        Log.e("NativeAdActivity", "Native ad failed to load: ${errorCode.message}")
    }

    override fun onAdWasClicked() {
        Log.d("NativeAdActivity", "Native ad clicked")
    }

    override fun onAdWasClicked(clickUrl: String, fallbackURL: String) {
        Log.d("NativeAdActivity", "Native ad clicked: $clickUrl")
    }

    override fun onAdWillLeaveApplication() {
        Log.d("NativeAdActivity", "Native ad will leave the app")
    }

    override fun onAdImpression() {
        Log.d("NativeAdActivity", "Native ad impression recorded")
    }

    override fun onAdAboutToExpire() {
        Log.d("NativeAdActivity", "Native ad is about to expire")
    }

    override fun onAdExpired() {
        Log.d("NativeAdActivity", "Native ad expired")
    }

    override fun onDestroy() {
        NativeAdSDK.unRegisterTracking(nativeContainer) // Stop tracking the native ad container
        nativeAdResponse = null
        super.onDestroy()
    }
}
```

### [Java](#tab/java1)

```java
public class NativeAdActivity extends AppCompatActivity
        implements NativeAdRequestListener, NativeAdEventListener {
    private NativeAdRequest nativeAdRequest;
    private NativeAdResponse nativeAdResponse;
    private View nativeContainer;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_native);

        nativeContainer = findViewById(R.id.native_ad_container);
        nativeAdRequest = new NativeAdRequest(this, "123456"); // Create a request for the placement ID
        nativeAdRequest.setListener(this); // Set the request listener
        nativeAdRequest.loadAd(); // Load the ad
    }

    @Override
    public void onAdLoaded(NativeAdResponse response) {
        nativeAdResponse = response;
        ((TextView) findViewById(R.id.native_ad_title)).setText(response.getTitle()); // Render the native ad title
        NativeAdSDK.registerTracking(response, nativeContainer, this); // Register tracking and event callbacks
    }

    @Override
    public void onAdFailed(ResultCode errorCode, ANAdResponseInfo adResponseInfo) {
        Log.e("NativeAdActivity", "Native ad failed to load: " + errorCode.getMessage());
    }

    @Override
    public void onAdWasClicked() {
        Log.d("NativeAdActivity", "Native ad clicked");
    }

    @Override
    public void onAdWasClicked(String clickUrl, String fallbackURL) {
        Log.d("NativeAdActivity", "Native ad clicked: " + clickUrl);
    }

    @Override
    public void onAdWillLeaveApplication() {
        Log.d("NativeAdActivity", "Native ad will leave the app");
    }

    @Override
    public void onAdImpression() {
        Log.d("NativeAdActivity", "Native ad impression recorded");
    }

    @Override
    public void onAdAboutToExpire() {
        Log.d("NativeAdActivity", "Native ad is about to expire");
    }

    @Override
    public void onAdExpired() {
        Log.d("NativeAdActivity", "Native ad expired");
    }

    @Override
    protected void onDestroy() {
        NativeAdSDK.unRegisterTracking(nativeContainer); // Stop tracking the native ad container
        nativeAdResponse = null;
        super.onDestroy();
    }
}
```

---

## Related

- [Show native ads on Android](show-native-ads-on-android.md)
- [Listener for onAdAboutToExpire on Android](listener-for-onadabouttoexpire-on-android.md)
- [Viewability measurement on Android](viewability-measurement-on-android.md)
