---
title: Show native ads on Android
description: Learn how to request, render, track, and release native ads in an Android app.
ms.custom: android-sdk
ms.date: 09/21/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: subramaniank
---

# Show native ads on Android

This article describes how to use `NativeAdRequest` and `NativeAdResponse` to show native ads in your Android app.

## Overview

Native ads let you render ad assets in views that match your app's design. To support this workflow, the Android SDK exposes the following classes, interfaces, and methods:

- `NativeAdRequest` loads an ad for a placement, and `NativeAdRequestListener` receives the result.
- `NativeAdResponse` provides the native assets returned by a successful request.
- `NativeAdSDK.registerTracking()` associates the rendered container with the response, while `NativeAdEventListener` receives impression and click events.

In the standard SDK flow, create and load a request, render the assets from the response, and then register the container for tracking.

- Keep references to the request, response, and container while the ad is displayed.
- Unregister the container before reusing it for another native ad and when the view is destroyed.

To customize the assets returned in a native ad response, see [Request specific assets with OpenRTB Native](#request-specific-assets-with-openrtb-native) or [Request specific assets with Native Assembly](#request-specific-assets-with-native-assembly).

> [!NOTE]
> For information about native impression counting, see [Impression counting methods](impression-counting-methods.md).

## Request a native ad

Use the following methods on `NativeAdRequest`:

| Method | Description |
|:---|:---|
| `NativeAdRequest(Context context, String placementId)` | Creates a native ad request for a placement ID. |
| `void setListener(NativeAdRequestListener listener)` | Sets the listener that receives the request result. |
| `void loadAd()` | Loads one native ad. |

## Access standard native response data

To use the standard native flow, load a `NativeAdRequest` without calling `setOpenRTBAssets()`. `NativeAdResponse` contains the assets and related metadata available for the selected ad.

Use the following methods on `NativeAdResponse`:

| Asset | Method | Default | Description |
|:---|:---|:---|:---|
| Title | `getTitle()` | Empty string | Returns the ad title. |
| Sponsored by | `getSponsoredBy()` | Empty string | Returns the advertiser or sponsor name. |
| Body text | `getDescription()` | Empty string | Returns the primary ad description. |
| Additional description | `getAdditionalDescription()` | Empty string | Returns the additional ad description. |
| Call to action | `getCallToAction()` | Empty string | Returns text for the call-to-action control. |
| Main image URL | `getImageUrl()` | Empty string | Returns the URL for loading the main image. |
| Main image size | `getImageSize()` | Width and height are `-1` | Returns the main image dimensions. |
| Main image | `getImage()` | `null` | Returns the preloaded main image. See [Configure image loading](#configure-image-loading). |
| Icon image URL | `getIconUrl()` | Empty string | Returns the URL for loading the icon image. |
| Icon image size | `getIconSize()` | Width and height are `-1` | Returns the icon image dimensions. |
| Icon image | `getIcon()` | `null` | Returns the preloaded icon image. See [Configure image loading](#configure-image-loading). |
| Rating | `getAdStarRating()` | `null` | Returns the rating value and scale for the advertised product or app. |
| Privacy URL | `getPrivacyLink()` | Empty string | Returns the privacy information URL supplied for the ad, when available. |

## Register tracking

After rendering the assets from `NativeAdResponse`, use `NativeAdSDK` to register the container for impression and click tracking:

| Method | Description |
|:---|:---|
| <code>void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>NativeAdEventListener listener)</code> | Registers the rendered container for impression tracking and makes the container clickable. |
| <code>void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>List&lt;View&gt; clickableViews, <wbr>NativeAdEventListener listener)</code> | Registers the rendered container for impression tracking and makes the listed views clickable. |
| <code>void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>NativeAdEventListener listener, <wbr>List&lt;View&gt; friendlyObstructions)</code> | Registers tracking with friendly obstructions. |
| <code>void registerTracking(<wbr>NativeAdResponse response, <wbr>View container, <wbr>List&lt;View&gt; clickableViews, <wbr>NativeAdEventListener listener, <wbr>List&lt;View&gt; friendlyObstructions)</code> | Registers tracking with specific clickable views and friendly obstructions. |
| `void unRegisterTracking(View container)` | Stops tracking the registered container and completes its viewability session. |

For information about registering friendly obstructions, see [Viewability measurement on Android](viewability-measurement-on-android.md).

## Example

### [Kotlin](#tab/kotlin1)

```kotlin
class NativeAdActivity : AppCompatActivity(), NativeAdRequestListener, NativeAdEventListener {
    private lateinit var nativeAdRequest: NativeAdRequest
    private var nativeAdResponse: NativeAdResponse? = null
    private lateinit var nativeContainer: View

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
        val mainImageUrl = response.imageUrl // Pass the main image URL to your app's image-loading implementation
        val iconImageUrl = response.iconUrl // Pass the icon image URL to your app's image-loading implementation
        findViewById<TextView>(R.id.native_ad_title).text = response.title // Render the title
        findViewById<TextView>(R.id.native_ad_sponsored_by).text = response.sponsoredBy // Render the sponsor name
        findViewById<TextView>(R.id.native_ad_body).text = response.description // Render the body text
        response.adStarRating?.let { rating ->
            findViewById<TextView>(R.id.native_ad_rating).text = "${rating.value}/${rating.scale}" // Render the rating
        }
        val privacyUrl = response.privacyLink // Get the privacy URL
        val callToActionButton = findViewById<Button>(R.id.native_ad_call_to_action)
        callToActionButton.text = response.callToAction // Render the call-to-action text

        NativeAdSDK.unRegisterTracking(nativeContainer) // Stop tracking any previous ad in the container
        NativeAdSDK.registerTracking(
            response,
            nativeContainer,
            listOf(callToActionButton),
            this
        ) // Track impressions and CTA clicks
        nativeContainer.visibility = View.VISIBLE
    }

    override fun onAdFailed(errorCode: ResultCode, adResponseInfo: ANAdResponseInfo?) {
        Log.e("NativeAdActivity", "Native ad failed to load: ${errorCode.message}")
    }

    override fun onAdImpression() = Unit
    override fun onAdWasClicked() = Unit
    override fun onAdWasClicked(clickUrl: String, fallbackURL: String) = Unit
    override fun onAdWillLeaveApplication() = Unit
    override fun onAdAboutToExpire() = Unit
    override fun onAdExpired() = Unit

    override fun onDestroy() {
        NativeAdSDK.unRegisterTracking(nativeContainer) // Stop tracking and complete the viewability session
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
        String mainImageUrl = response.getImageUrl(); // Pass the main image URL to your app's image-loading implementation
        String iconImageUrl = response.getIconUrl(); // Pass the icon image URL to your app's image-loading implementation
        ((TextView) findViewById(R.id.native_ad_title)).setText(response.getTitle()); // Render the title
        ((TextView) findViewById(R.id.native_ad_sponsored_by)).setText(response.getSponsoredBy()); // Render the sponsor name
        ((TextView) findViewById(R.id.native_ad_body)).setText(response.getDescription()); // Render the body text
        NativeAdResponse.Rating rating = response.getAdStarRating();
        if (rating != null) {
            ((TextView) findViewById(R.id.native_ad_rating)).setText(
                rating.getValue() + "/" + rating.getScale()); // Render the rating
        }
        String privacyUrl = response.getPrivacyLink(); // Get the privacy URL
        Button callToActionButton = findViewById(R.id.native_ad_call_to_action);
        callToActionButton.setText(response.getCallToAction()); // Render the call-to-action text

        NativeAdSDK.unRegisterTracking(nativeContainer); // Stop tracking any previous ad in the container
        NativeAdSDK.registerTracking(
            response,
            nativeContainer,
            Arrays.asList(callToActionButton),
            this
        ); // Track impressions and CTA clicks
        nativeContainer.setVisibility(View.VISIBLE);
    }

    @Override
    public void onAdFailed(ResultCode errorCode, ANAdResponseInfo adResponseInfo) {
        Log.e("NativeAdActivity", "Native ad failed to load: " + errorCode.getMessage());
    }

    @Override public void onAdImpression() {}
    @Override public void onAdWasClicked() {}
    @Override public void onAdWasClicked(String clickUrl, String fallbackURL) {}
    @Override public void onAdWillLeaveApplication() {}
    @Override public void onAdAboutToExpire() {}
    @Override public void onAdExpired() {}

    @Override
    protected void onDestroy() {
        NativeAdSDK.unRegisterTracking(nativeContainer); // Stop tracking and complete the viewability session
        nativeAdResponse = null;
        super.onDestroy();
    }
}
```

---

## Extended Native Ad Assets

In addition to the standard native ad flow, your app can optionally access extended assets through OpenRTB Native or Native Assembly. If you set `openRTBAssets`, the OpenRTB Native request takes precedence over the Native Assembly configuration associated with the placement.

For either workflow, your app can parse the exposed asset object directly instead of using the normalized asset accessors on `NativeAdResponse`. Keep the `NativeAdResponse` instance to register the rendered container for tracking and receive native ad events.

| Asset | [OpenRTB Native](#request-specific-assets-with-openrtb-native) access | [Native Assembly](#request-specific-assets-with-native-assembly) access | Description |
|:---|:---|:---|:---|
| VAST video | `getVastXml()` | `getVastXml()` | Returns the VAST video markup. |
| Likes | `getOpenRTBNative()` by request ID | `getNativeElements()` with `likes` | Returns the number of likes. |
| Downloads | `getOpenRTBNative()` by request ID | `getNativeElements()` with `downloads` | Returns the number of downloads. |
| Price | `getOpenRTBNative()` by request ID | `getNativeElements()` with `price` | Returns the product price. |
| Sale price | `getOpenRTBNative()` by request ID | `getNativeElements()` with `saleprice` | Returns the discounted product price. |
| Phone | `getOpenRTBNative()` by request ID | `getNativeElements()` with `phone` | Returns the advertiser phone number. |
| Address | `getOpenRTBNative()` by request ID | `getNativeElements()` with `address` | Returns the advertiser address. |
| Display URL | `getOpenRTBNative()` by request ID | `getNativeElements()` with `displayurl` | Returns the advertiser-facing display URL. |
| Click URL | `getOpenRTBNative()` with `link.url` | `getNativeElements()` with `link.url` | Returns the primary click destination. |
| Click fallback URL | `getOpenRTBNative()` with `link.fallback` | `getNativeElements()` with `link.fallback_url` | Returns the fallback click destination. |
| Custom extension | `getOpenRTBNative()` with `ext` | Not applicable | Returns response-level extension data defined by the demand partner. |

### Request specific assets with OpenRTB Native

> [!NOTE]
> OpenRTB Native isn't available for all members. Contact your account representative or Microsoft Advertising Support to confirm availability. Don't include `eventtrackers` in `openRTBAssets`; the Android SDK adds the supported event trackers.

**`NativeAdRequest`:** Use `openRTBAssets` to describe the assets your app needs according to OpenRTB Native 1.2. You can specify image sizes, text lengths, video, and custom assets. Assign each asset an `id` so you can match it to the value returned in the response. You can also add custom data through `ext` using keys and values agreed with your demand partner. For available fields and values, see the [IAB OpenRTB Native Ads Specification 1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf). Set `openRTBAssets` before calling `loadAd()`.

Use the following method on `NativeAdRequest`:

| Method | Description |
|:---|:---|
| `void setOpenRTBAssets(JSONObject openRTBAssets)` | Sets the OpenRTB Native 1.2 request object that defines the requested assets and constraints. |

**`NativeAdResponse`:** Whenever possible, the SDK maps standard assets to the corresponding accessors. The complete OpenRTB Native response is also available through `getOpenRTBNative()`, where you can find returned assets by the IDs used in the request.

Use the following method on `NativeAdResponse`:

| Method | Description |
|:---|:---|
| `JSONObject getOpenRTBNative()` | Returns the complete OpenRTB Native response, or an empty `JSONObject` when unavailable. |

### [Kotlin](#tab/kotlin2)

```kotlin
private fun loadOpenRTBNativeAd() {
    nativeAdRequest = NativeAdRequest(this, "123456") // Create a request for the placement ID
    nativeAdRequest.listener = this // Set the request listener
    val openRTBAssets = JSONObject().apply {
        put("ver", "1.2") // Set the OpenRTB Native version
        put("privacy", 1) // Request privacy information
        put("ext", JSONObject().put("foo", "bar")) // Add a custom request extension
        put("assets", JSONArray().apply {
            put(JSONObject("""{"id":1,"required":1,"title":{"len":300}}""")) // Request title
            put(JSONObject("""{"id":2,"required":1,"data":{"type":2}}""")) // Request body text
            put(JSONObject("""{"id":3,"required":0,"data":{"type":1}}""")) // Request sponsor name
            put(JSONObject("""{"id":4,"required":0,"img":{"type":3}}""")) // Request main image
            put(JSONObject("""{"id":5,"required":0,"data":{"type":12}}""")) // Request CTA text
            put(JSONObject("""{"id":6,"required":0,"img":{"type":1,"hmin":50,"wmin":50}}""")) // Request icon
            put(JSONObject("""{"id":7,"required":0,"data":{"type":4}}""")) // Request likes
            put(JSONObject("""{"id":8,"required":0,"data":{"type":6}}""")) // Request price
            put(JSONObject("""{"id":9,"required":0,"data":{"type":11}}""")) // Request display URL
        })
    }
    nativeAdRequest.openRTBAssets = openRTBAssets // Set requested OpenRTB Native assets
    nativeAdRequest.loadAd() // Load the ad
}

override fun onAdLoaded(response: NativeAdResponse) {
    val openRTBNative = response.openRTBNative
    val responseAssets = openRTBNative.optJSONArray("assets")
    val assetsById = mutableMapOf<Int, JSONObject>()
    for (index in 0 until (responseAssets?.length() ?: 0)) {
        val asset = responseAssets?.optJSONObject(index)
        if (asset != null) {
            assetsById[asset.optInt("id")] = asset
        }
    }
    val title = response.title // Or: assetsById[1]?.optJSONObject("title")?.optString("text")
    val body = response.description // Or: assetsById[2]?.optJSONObject("data")?.optString("value")
    val mainImageUrl = response.imageUrl // Or: assetsById[4]?.optJSONObject("img")?.optString("url")
    val callToAction = response.callToAction // Or: assetsById[5]?.optJSONObject("data")?.optString("value")
    val iconImageUrl = response.iconUrl // Or: assetsById[6]?.optJSONObject("img")?.optString("url")
    val likes = assetsById[7]?.optJSONObject("data")?.optString("value") // Match request ID 7
    val price = assetsById[8]?.optJSONObject("data")?.optString("value") // Match request ID 8
    val displayUrl = assetsById[9]?.optJSONObject("data")?.optString("value") // Match request ID 9
    val customExtension = openRTBNative.optJSONObject("ext")
    val customValue = customExtension?.optString("foo") // Read a custom response extension
    val link = openRTBNative.optJSONObject("link")
    val clickUrl = link?.optString("url")
    val clickFallbackUrl = link?.optString("fallback")
}
```

### [Java](#tab/java2)

```java
private void loadOpenRTBNativeAd() {
    nativeAdRequest = new NativeAdRequest(this, "123456"); // Create a request for the placement ID
    nativeAdRequest.setListener(this); // Set the request listener
    JSONArray assets = new JSONArray()
        .put(new JSONObject().put("id", 1).put("required", 1)
            .put("title", new JSONObject().put("len", 300))) // Request title
        .put(new JSONObject().put("id", 2).put("required", 1)
            .put("data", new JSONObject().put("type", 2))) // Request body text
        .put(new JSONObject().put("id", 3).put("required", 0)
            .put("data", new JSONObject().put("type", 1))) // Request sponsor name
        .put(new JSONObject().put("id", 4).put("required", 0)
            .put("img", new JSONObject().put("type", 3))) // Request main image
        .put(new JSONObject().put("id", 5).put("required", 0)
            .put("data", new JSONObject().put("type", 12))) // Request CTA text
        .put(new JSONObject().put("id", 6).put("required", 0)
            .put("img", new JSONObject().put("type", 1).put("hmin", 50).put("wmin", 50))) // Request icon
        .put(new JSONObject().put("id", 7).put("required", 0)
            .put("data", new JSONObject().put("type", 4))) // Request likes
        .put(new JSONObject().put("id", 8).put("required", 0)
            .put("data", new JSONObject().put("type", 6))) // Request price
        .put(new JSONObject().put("id", 9).put("required", 0)
            .put("data", new JSONObject().put("type", 11))); // Request display URL
    JSONObject openRTBAssets = new JSONObject()
        .put("ver", "1.2")
        .put("privacy", 1)
        .put("ext", new JSONObject().put("foo", "bar")) // Add a custom request extension
        .put("assets", assets);
    nativeAdRequest.setOpenRTBAssets(openRTBAssets); // Set requested OpenRTB Native assets
    nativeAdRequest.loadAd(); // Load the ad
}

@Override
public void onAdLoaded(NativeAdResponse response) {
    JSONObject openRTBNative = response.getOpenRTBNative();
    JSONArray responseAssets = openRTBNative.optJSONArray("assets");
    Map<Integer, JSONObject> assetsById = new HashMap<>();
    if (responseAssets != null) {
        for (int index = 0; index < responseAssets.length(); index++) {
            JSONObject asset = responseAssets.optJSONObject(index);
            if (asset != null) {
                assetsById.put(asset.optInt("id"), asset);
            }
        }
    }
    String title = response.getTitle(); // Or: assetsById.get(1).optJSONObject("title").optString("text")
    String body = response.getDescription(); // Or: assetsById.get(2).optJSONObject("data").optString("value")
    String mainImageUrl = response.getImageUrl(); // Or: assetsById.get(4).optJSONObject("img").optString("url")
    String callToAction = response.getCallToAction(); // Or: assetsById.get(5).optJSONObject("data").optString("value")
    String iconImageUrl = response.getIconUrl(); // Or: assetsById.get(6).optJSONObject("img").optString("url")
    JSONObject likesAsset = assetsById.get(7);
    JSONObject priceAsset = assetsById.get(8);
    JSONObject displayUrlAsset = assetsById.get(9);
    JSONObject likesData = likesAsset != null ? likesAsset.optJSONObject("data") : null;
    JSONObject priceData = priceAsset != null ? priceAsset.optJSONObject("data") : null;
    JSONObject displayUrlData = displayUrlAsset != null ? displayUrlAsset.optJSONObject("data") : null;
    String likes = likesData != null ? likesData.optString("value") : null; // Match request ID 7
    String price = priceData != null ? priceData.optString("value") : null; // Match request ID 8
    String displayUrl = displayUrlData != null ? displayUrlData.optString("value") : null; // Match request ID 9
    JSONObject customExtension = openRTBNative.optJSONObject("ext");
    String customValue = customExtension != null ? customExtension.optString("foo") : null; // Read a custom response extension
    JSONObject link = openRTBNative.optJSONObject("link");
    String clickUrl = link != null ? link.optString("url") : null;
    String clickFallbackUrl = link != null ? link.optString("fallback") : null;
}
```

---

### Request specific assets with Native Assembly

**`NativeAdRequest`:** No Native Assembly-specific request configuration is required in your app. Native Assembly is configured for the placement in Microsoft Monetize and is used when `openRTBAssets` isn't set. For this workflow, the SDK uses only the **Creative Asset Specifications** from the Native Assembly associated with the placement. The HTML, CSS, and JavaScript from the **Renderer** tab aren't used; your app renders the returned assets. Renderer code applies only to the Banner Native rendering workflow. For more information, see [Native Assembly Renderer for Android](native-assembly-renderer-for-android.md). We recommend using OpenRTB Native when it's available. For setup instructions, see [Configuring a Native Assembly](../monetize/configuring-a-native-assembly.md).

**`NativeAdResponse`:** Get the value for `NativeAdResponse.NATIVE_ELEMENT_OBJECT` from `getNativeElements()`, cast it to a `JSONObject`, and then read each asset by its field name. Check that a field exists before using it because the creative might omit it.

Use the following method on `NativeAdResponse`:

| Method | Description |
|:---|:---|
| `HashMap<String, Object> getNativeElements()` | Returns all elements in the native ad response. |

### [Kotlin](#tab/kotlin3)

```kotlin
val nativeElements = response.nativeElements[NativeAdResponse.NATIVE_ELEMENT_OBJECT] as? JSONObject
val title = response.title // Or: nativeElements?.optString("title")
val body = response.description // Or: nativeElements?.optString("desc")
val mainImageUrl = response.imageUrl // Or: nativeElements?.optJSONObject("main_img")?.optString("url")
val iconImageUrl = response.iconUrl // Or: nativeElements?.optJSONObject("icon")?.optString("url")
val callToAction = response.callToAction // Or: nativeElements?.optString("ctatext")
val likes = nativeElements?.optString("likes")
val price = nativeElements?.optString("price")
val link = nativeElements?.optJSONObject("link")
val clickUrl = link?.optString("url")
val clickFallbackUrl = link?.optString("fallback_url")
```

### [Java](#tab/java3)

```java
Object element = response.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT);
if (element instanceof JSONObject) {
    JSONObject nativeElements = (JSONObject) element;
    String title = response.getTitle(); // Or: nativeElements.optString("title")
    String body = response.getDescription(); // Or: nativeElements.optString("desc")
    String mainImageUrl = response.getImageUrl(); // Or: nativeElements.optJSONObject("main_img").optString("url")
    String iconImageUrl = response.getIconUrl(); // Or: nativeElements.optJSONObject("icon").optString("url")
    String callToAction = response.getCallToAction(); // Or: nativeElements.optString("ctatext")
    String likes = nativeElements.optString("likes");
    String price = nativeElements.optString("price");
    JSONObject link = nativeElements.optJSONObject("link");
    String clickUrl = link != null ? link.optString("url") : null;
    String clickFallbackUrl = link != null ? link.optString("fallback_url") : null;
}
```

---

## Configure image loading

Native ad responses can include URLs for a main image and an icon. Use these URLs with your app's image-loading implementation, or enable SDK preloading before calling `loadAd()` to receive downloaded `Bitmap` objects. Preloading is disabled by default.

Use the following methods on `NativeAdRequest`:

| Method | Description |
|:---|:---|
| `void shouldLoadImage(boolean shouldLoadImage)` | Sets whether the SDK preloads the main image. |
| `void shouldLoadIcon(boolean shouldLoadIcon)` | Sets whether the SDK preloads the icon image. |

### [Kotlin](#tab/kotlin4)

```kotlin
nativeAdRequest.shouldLoadImage(true) // Preload the main image
nativeAdRequest.shouldLoadIcon(true) // Preload the icon image
nativeAdRequest.loadAd() // Load the ad

val mainImage = response.image // Get the preloaded main image
val iconImage = response.icon // Get the preloaded icon image
```

### [Java](#tab/java4)

```java
nativeAdRequest.shouldLoadImage(true); // Preload the main image
nativeAdRequest.shouldLoadIcon(true); // Preload the icon image
nativeAdRequest.loadAd(); // Load the ad

Bitmap mainImage = response.getImage(); // Get the preloaded main image
Bitmap iconImage = response.getIcon(); // Get the preloaded icon image
```

---

## Related

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Get Facebook Demand for Native on Android](get-facebook-demand-for-native-on-android.md)
- [Mediate with Android SDK Instructions](mediate-with-android-sdk-instructions.md)
