---
title: Show Native Ads on Android
description: Native ads give you the ability to create ads that are customized to match the look and feel of the rest of your application. This page describes our Native Ads API at a high level with usage examples.
ms.custom: android-sdk
ms.date: 10/28/2023
---


# Show native ads on Android

> [!NOTE]
> Native impression counting methodology follows the count-on-render methodology that is used for banner creatives - an impression will fire as soon as the native advertisement renders, regardless of its length of time on the screen. This will ensure greater accuracy and better deliverability thus improving overall yield.

Native ads give you the ability to create ads that are customized to match the look and feel of the rest of your application. This page describes our Native Ads API at a high level, and includes a usage example.

Native networks supported through **mediation**:

- Facebook
- AdMob and DFP

In order to serve native ads, you will send a native ad request, and receive a native ad response. For Android 9 and above and API v. 28 and above, the request must be HTTPS by default in order to accurately track viewability. You can enable HTTPS with `useHttps(true)`.

In the example code below, we:

- Set up a request object and supply it with either:
  - The placement ID (as shown in the example code below), OR

  - A combination of inventory code and member ID:

    ``` 
    public NativeAdRequest nativeAdRequest= new NativeAdRequest(context, "PLACEMENT_ID");
    //public NativeAdRequest nativeAdRequest= new NativeAdRequest(context, "INVENTORY_CODE", MEMBER_ID);
    ```

- Optionally, you can set the `renderer_id`  for this `NativeAdRequest`. (For more on `renderer_id` see [Native Layout Service](../digital-platform-api/native-layout-service.md).) The `renderer_id` needs to be specified in order for vastxml, likes, downloads, saleprice, phone, address, and display URL to be returned in the `NativeAdResponse`.  

  ``` 
  nativeAdRequest.setRendererId(RENDERER_ID);
  ```

- Register a listener that will signal native ad events such as clicks (NativeAdEventListener).

- Register a listener to signal the state of the native request: success or failure. The listener must implement the `NativeAdRequestListener` interface.

- If the request is successful (i.e., `NativeAdListener.onAdLoaded()` fires), native ad assets are loaded in the `NativeAdResponse` object which can be used in views that match the native look of the app. Then register the parent or container view of these views to enable impression and click tracking.

- Unregister the native ad view after you have completed the workflow. When the unregister method is called, OMID viewability script of Xandr Mobile SDK generates a bulk report of the OMID session during the worflow. Therefore, it is important for the publishers to implement this API which facilitates an accurate measure on the viewability.

> [!NOTE]
> Maintain references to native views and native response objects. Maintain references to native views and native response objects.
>
> It is your responsibility to keep a reference to the native ad view and `NativeAdResponse` object if necessary.

``` 
public class MyActivity extends Activity {
 
    Context activityContext;
    NativeAdResponse nativeAdResponse;
    LinearLayout container;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
 
        activityContext = this;
 
        // Create a NativeAdRequest object
        NativeAdRequest adRequest = new NativeAdRequest(activityContext, "123456"); // Placement ID
         
        // Optionally set the renderer_id
        //adRequest.setRendererId(123);
 
        // Create a listener for ad events
        NativeAdEventListener adEventListener = new
                NativeAdEventListener() {
                    @Override
                    public void onAdWasClicked() {
                        // Do something when the view is clicked
                    }
 
                    @Override
                    public void onAdWillLeaveApplication() {
                        // Do something when the ad is taking user away from current app
                    }
 
                    @Override
                    public void onAdWasClicked(String clickUrl, String fallbackURL) {
                        // Handle Click URL
                    }
                };
 
        // Whether to pre-load the native ad's icon and main image
        adRequest.shouldLoadIcon(true);
        adRequest.shouldLoadImage(true);
 
        adRequest.setListener(new NativeAdRequestListener() {
            @Override
            public void onAdLoaded(NativeAdResponse response) {
                nativeAdResponse = response;
                // Cover image
                ImageView imageView = new ImageView(activityContext);
                imageView.setImageBitmap(response.getImage());
 
                // Icon image
                ImageView iconView = new ImageView(activityContext);
                iconView.setImageBitmap(response.getIcon());
 
                // Title
                TextView title = new TextView(activityContext);
                title.setText(response.getTitle());
 
                // Main text
                TextView description = new TextView(activityContext);
                description.setText(response.getDescription());
 
                // Text that indicates a call to action -- for example, to install an app
                TextView callToAction = new TextView(activityContext);
                callToAction.setText(response.getCallToAction());
 
                // Create a container (a parent view that holds all the
                // views for native ads)
                LinearLayout container = new LinearLayout(activityContext);
                container.addView(iconView);
                container.addView(title);
 
                // Add the native ad container to the view hierarchy
                LinearLayout ad_frame = findViewById(R.id.native_ad_frame);
                ad_frame.addView(container);
            }
 
            @Override
            public void onAdFailed(ResultCode errorcode) {
 
            }
        });
 
        // Call loadAd() to request a response once
        adRequest.loadAd();
 
        // Register native views for click and impression tracking.  The
        // adEventListener is the listener created above; it can be null if
        // you don't want to receive notifications about click events.
        // Impressions and clicks won't be counted if the view is not registered.
        NativeAdSDK.registerTracking(nativeAdResponse, container, adEventListener);
 
        // It's your responsibility to keep a reference to the view
        // and NativeAdResponse object if necessary.
        // Once done with the native ad view, call the following method to
        // unregister that view.
        NativeAdSDK.unRegisterTracking(container);
    }
}
    
```

## Fields supported in native

As of version 5.0 of the Mobile SDK, support for native assets is aligned with how native creatives are set up in Xandr's UI.

If you are still using Legacy Native in, you will need to move to "New" Native for your creatives.

The following is a comprehensive list of native assets supported in the SDKs.

| Asset | Supported Pre 5.0? | Supported Post 5.0? | v5.0+ API-Usage Example |
|--|--|--|--|
| Image, Width, Height | Yes, Yes, Yes | Yes, Yes, Yes | `nativeAdResponse.getImage()`;<br> `nativeAdResponse.getImageSize()`; <br> `nativeAdResponse.getImageUrl();` |
| Icon+Width+Height | Yes, No, No | Yes, Yes, Yes | `nativeAdResponse.getIcon()`; <br> `nativeAdResponse.getIconSize()`; <br> `nativeAdResponse.getIconUrl();` |
| Title | Yes | Yes | `nativeAdResponse.getTitle();` |
| Sponsored by | Yes | Yes | `nativeAdResponse.getSponsoredBy();` |
| Body text | Yes | Yes | `nativeAdResponse.getDescription();` |
| Desc2 | Yes | Yes | `nativeAdResponse.getAdditionalDescription();` |
| Call-to-action | Yes | Yes | `nativeAdResponse.getCallToAction();` |
| Rating, Scale | Yes, Yes | Yes, No | `nativeAdResponse.getAdStarRating();` |
| Likes | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```; <br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Downloads | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Price | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Sale Price | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Phone | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Address | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Display URL | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Click URL | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Click Fallback URL | No | Yes (json only) | ```if((nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS) &&. (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT)) instanceof JSONObject){ JSONObject nativeResponseJSON = (JSONObject) (nativeAdResponse.getNativeElements().get(NativeAdResponse.NATIVE_ELEMENT_OBJECT))```;<br><br>```String likes = JsonUtil.getJSONString(nativeResponseJSON,"likes"); String downloads = JsonUtil.getJSONString(nativeResponseJSON,"downloads"); String price = JsonUtil.getJSONString(nativeResponseJSON,"price"); String saleprice = JsonUtil.getJSONString(nativeResponseJSON,"saleprice"); String phone = JsonUtil.getJSONString(nativeResponseJSON,"phone"); String address = JsonUtil.getJSONString(nativeResponseJSON,"address"); String displayurl = JsonUtil.getJSONString(nativeResponseJSON,"displayurl"); // To Get clickUrl String clickUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("url"); //To Get clickFallbackUrl String clickFallbackUrl = JsonUtil.getJSONObject(nativeResponseJSON,"link").getString("fallback_url"); }``` |
| Privacy URL | No | Yes | `nativeAdResponse.getPrivacyLink();` |
| Video | No | Yes | `nativeAdResponse.getVastXml();` |
| Custom | Yes | No |  |
| Context | Yes | No |  |
| Full text | Yes | No |  |

## OpenRTB Native

OpenRTB Native refers to using the OpenRTB Native Asset specification in NativeAdRequest and NativeAdResponse classes, allowing for more flexible and standardized ad requests and responses.
For more information on OpenRTB Native 1.2 spec standards, see [OpenRTB Native Ads Specification.1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf).

> [!NOTE]
> OpenRTB Native is not available for all members. Please work with your Account Manager or contact Support if you have any questions.

### ORTB in NativeAdRequest

To use OpenRTB Native, the app needs to specify OpenRTB Native assets in the NativeAdRequest using the setOpenRTBAssets(JSONObject openRTBAssets) method. The contents of this field should be an OpenRTB Native request, following the OpenRTB Native 1.2 request markup.

### Code Sample Java for Request

```
NativeAdRequest nativeAdRequest = new NativeAdRequest(context, "PLACEMENT_ID");
String ortbJSONString = "{\"ver\":\"1.2\",\"assets\":[{\"id\":1,\"required\":1,\"title\":{\"len\":300}},{\"id\":2,\"required\":1,\"data\":{\"type\":2}},{\"id\":3,\"required\":1,\"data\":{\"type\":1}},{\"id\":4,\"required\":1,\"image\":{\"type\":3}},{\"id\":5,\"required\":0,\"data\":{\"type\":555,\"len\":45}}]}";
nativeAdRequest.setOpenRTBAssets(new JSONObject(ortbJSONString));
```

### Code Sample Kotlin for Request

```

var nativeAdRequest = NativeAdRequest(context, "PLACEMENT_ID")
val ortbJSONString = "{\"ver\":\"1.2\",\"assets\":[{\"id\":1,\"required\":1,\"title\":{\"len\":300}},{\"id\":2,\"required\":1,\"data\":{\"type\":2}},{\"id\":3,\"required\":1,\"data\":{\"type\":1}},{\"id\":4,\"required\":1,\"image\":{\"type\":3}},{\"id\":5,\"required\":0,\"data\":{\"type\":555,\"len\":45}}]}"
nativeAdRequest.openRTBAssets = JSONObject(ortbJSONString);
```
>[!NOTE]
> The app does not need to specify the eventtrackers array. SDK automatically populates the eventtrackers array with the values it supports. Even if the app provides a value, it will be overridden by the SDK.

## ORTB in NativeAdResponse
ORTB in response corresponds to the raw ORTB Native JSON, which is exposed to the app using the public JSONObject getOpenRTBNative() method in the NativeAdResponse class. Like the request, the response JSONObject will follow the OpenRTB Native 1.2 response markup, see [OpenRTB Native Ads Specification.1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf) for details.


In addition to exposing the raw ORTB Native response JSONObject via getOpenRTBNative(), the SDK also parses and makes available standard ORTB Native response assets (img, title, video, and data) using methods such as getTitle(), getDescription(), getImageUrl(), getImage(), getImageSize(), getIconUrl(), getIcon(), getIconSize(), getCallToAction(), getAdStarRating(), getSponsoredBy(), getVastXml(), and getPrivacyLink(). The SDK also automatically handles impression, viewability, and click tracking.

> [!NOTE]
> The app should register the view in which the native ad is rendered with the SDK. SDK will handle impression, click,
and viewability tracking. App will not receive eventtrackers, imptrackers, jstracker, or clicktrackers in the ORTB Native response JSONObject.

### Code Sample Java for response

```
@Override
public void onAdLoaded(NativeAdResponse nativeAdResponse) {

    // Network type Network.APPNEXUS_ORTB indicates the response is ORTB
    if (nativeAdResponse.getNetworkIdentifier() == NativeAdResponse.Network.APPNEXUS_ORTB) {
        JSONObject ortbNativeResponseJSON = nativeAdResponse.getOpenRTBNative();

        // App has the option to either
        // 1. Use the parsed title, description, etc., which the SDK readily makes available
        // and dip into the ORTB Native response JSON for non-parsed/custom values
        // OR
        // 2. Handle all the ORTB Native response JSON response parsing in the app

        // Accessing title, description etc using the getters exposed in
        // NativeAdResponse class
        String title = nativeAdResponse.getTitle();
        String description = nativeAdResponse.getDescription();
        String imageUrl = nativeAdResponse.getImageUrl();
        NativeAdResponse.ImageSize imageSize = nativeAdResponse.getImageSize();
        
        
        // Parsing ORTB Native resposnse JSON
        // Extract "assets" array
        JSONArray assetsArray = ortbNativeResponseJSON.getJSONArray("assets");
        for (int i = 0; i < assetsArray.length(); i++) {
            JSONObject asset = assetsArray.getJSONObject(i);
            // This id will match the id provided in the request.
            // This id is essential for matching the various data assets in the request
            // with the response.            
            int id = asset.getInt("id");
            System.out.println("Asset ID: " + id); 

            // Check for "title"
            if (asset.has("title")) {
                String assetTitle = asset.getJSONObject("title").getString("text");
                System.out.println("Title: " + assetTitle);
            }

            // Check for "data"
            if (asset.has("data")) {
                String data = asset.getJSONObject("data").getString("value");
                System.out.println("Data: " + data);
            }

            // Check for "image"
            if (asset.has("image")) {
                JSONObject image = asset.getJSONObject("image");
                String url = image.getString("url");
                int width = image.getInt("w");
                int height = image.getInt("h");
                System.out.println("Image URL:"+url+",Width:"+width+",Height:"+height);
            }
        }
    }
}
```

### Code Sample Kotlin for response

```

override fun onAdLoaded(nativeAdResponse: NativeAdResponse) {

    // Network type Network.APPNEXUS_ORTB indicate the response is ORTB
    if(nativeAdResponse.networkIdentifier == NativeAdResponse.Network.APPNEXUS_ORTB) {
        var ortbNativeResponseJSON = nativeAdResponse.openRTBNative

        // App has the option to either
        // 1. Use the parsed title,description etc which the SDK readily makes available
        // and dip into the ORTB Native response JSON for non-parsed/custom values
        // OR
        // 2. Handle all the ORTB Native response JSON response parsing in the app

        // Accessing title, description etc using the getters exposed in
        // NativeAdResponse class
        nativeAdResponse.title
        nativeAdResponse.description
        nativeAdResponse.imageUrl
        nativeAdResponse.imageSize


        // Parsing ORTB Native resposnse JSON
        // Extract "assets" array
        val assetsArray = ortbNativeResponseJSON.getJSONArray("assets")
        for (i in 0 until assetsArray.length()) {
            val asset = assetsArray.getJSONObject(i)
            // This id will match the id provide in request,
            // This id is essential for matching the various data assets in req with response            
            val id = asset.getInt("id")
            println("Asset ID: $id") 

            // Check for "title"
            if (asset.has("title")) {
                val title = asset.getJSONObject("title").getString("text")
                println("Title: $title")
            }

            // Check for "data"
            if (asset.has("data")) {
                val data = asset.getJSONObject("data").getString("value")
                println("Data: $data")
            }

            // Check for "image"
            if (asset.has("image")) {
                val image = asset.getJSONObject("image")
                val url = image.getString("url")
                val width = image.getInt("w")
                val height = image.getInt("h")
                println("Image URL: $url, Width: $width, Height: $height")
            }
        }
    }
```

### Example: ORTB Native response JSONObject structure in NativeAdResponse

```

 {
       "ver": "1.2",
       "assets": [
      {
          "id": 1,
          "title": {
              "text": "Sample Title here."
          }
       },{    
          "id": 2,
          "data": {
              "value": "Sample description text here."
           }
      }, {
          "id": 3,
          "data": {
              "value": "Sample Sponsored by text here."
          }
      }, {
          "id": 4,
          "image": {
              "url": "https://sample.img.url/here.jpg",
              "w": 123,
              "h": 234
          }
      }, {
          "id": 5,
          "data": {
              "value": "Sample disclaimer value here."
          }
      }
   ],
  // remaining ortb native 1.2 response fields would be here;
  // ie for link,privacy etc if available
} 
```



## Related topics

- [Android SDK Integration Instructions](android-sdk-integration-instructions.md)
- [Get Facebook Demand for Native on Android](get-facebook-demand-for-native-on-android.md)
- [Mediate with Android SDK Instructions](mediate-with-android-sdk-instructions.md)
