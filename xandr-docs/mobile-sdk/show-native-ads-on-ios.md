---
title: Show Native Ads on iOS
description: Native ads give you the ability to create ads that are customized to match the look and feel of the rest of your application. Learn how to serve native ads in this page using the native ad request and native ad response.  
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Show Native Ads on iOS

## Overview

Native ads give you the ability to create ads that are customized to match the look and feel of the rest of your application. This article describes Mobile SDK Native Ads API at a high level, and includes an usage example. <!--For a complete reference, see the inline documentation in the code.-->

Native networks that supported through **mediation** for native ads are:

- Facebook
- Google AdMob and Google DoubleClick for Publishers (Google DFP)

In order to serve native ads, you will send a "native ad request" and receive a "native ad response" as explained in the following section.

> [!NOTE]
> Keep a reference to the `ANNativeAdRequest` and `ANNativeAdResponse` objects that you create, otherwise they will go out of scope and cause unexpected behavior.

## Process

- Set up a request object, and set some of its properties such as the placement ID and whether to pre-load the ad's icon image.
- Optionally, set the renderer_id for this NativeAdRequest. (For more on renderer_id see see [Native Layout Service](../digital-platform-api/native-layout-service.md).) The renderer_id needs to be specified for vastxml, likes, downloads, saleprice, phone, address, display URL to be returned in the NativeAdResponse.
- Assuming the request is successful, we load the native ad assets from the response into the view and register it so that we can track user interactions such as clicks.

## Request

First, we set up the request object and set some of its properties such as the placement ID and whether to pre-load the ad's icon image:

``` 
ANNativeAdRequest *request = [[ANNativeAdRequest alloc] init];
request.placementId = @"123456";
request.rendererId = 123;
request.gender = ANGenderMale;
request.shouldLoadIconImage = YES;
request.shouldLoadMainImage = YES;
request.delegate = self;
[request loadAd];
```

## Response

Assuming the request is successful, we load the native ad assets from the response into the view and register it so that we can track user interactions such as clicks:

``` 
- (void)adRequest:(ANNativeAdRequest *)request didReceiveResponse:(ANNativeAdResponse *)response {
      // (code which loads the view)
      MyDummyView *view;
      view.title.text = response.title;
      view.text.text = response.body;
      view.iconImageView.image = response.iconImage;
      view.mainImageView.image = response.mainImage;
      [view.callToActionButton setTitle:response.callToAction forState:UIControlStateNormal];
 
      response.delegate = self;
 
      [response registerViewForTracking:view
                 withRootViewController:self
                         clickableViews:@[view.callToActionButton, view.mainImageView]
                                  error:nil];
 }
```

In this example response, we use several elements of a native ad:

- A title
- An icon image
- The main ad image
- Bodytext
- A "call to action" button that the user can click to convert

## Fields supported in Native

As of version 5.0 of the Mobile SDK, support for native assets is aligned with how native creatives are set up in the application.

If you are still using Legacy Native in the application, you will need to move to "New" Native for your creatives.

The following is a comprehensive list of native assets supported in the SDKs.

| Asset | Supported Pre 5.0? | Supported Post 5.0? | v5.0+ API-Usage Example |
|--|--|--|--|
| Image, Width, Height | Yes, Yes, Yes | Yes, Yes, Yes | `response.mainImage;` <br> `response.mainImageSize;` <br> `response.mainImageURL;` |
| Icon+Width+Height | Yes, No, No | Yes, Yes, Yes | `response.iconImage;`<br> `response.iconImageURL;` <br> `response.iconImageSize;` |
| Title | Yes | Yes | `response.title;` |
| Sponsored by | Yes | Yes | `response.sponsoredBy;` |
| Body text | Yes | Yes | `response.body;` |
| Desc2 | Yes | Yes | `response.additionalDescription;` |
| Call-to-action | Yes | Yes | `response.callToAction;` |
| Rating, Scale | Yes, Yes | Yes, No | `response.rating;` |
| Likes | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Downloads | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Price | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Sale Price | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Phone | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Address | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Display URL | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Click URL | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Click Fallback URL | No | Yes (json only) | ```NSDictionary *customElements = response.customElements[@"ELEMENT"]; if(customElements){ NSString *likes = customElements[@"likes"] NSString *downloads = customElements[@"downloads"] NSString *price = customElements[@"price"] NSString *saleprice = customElements[@"saleprice"] NSString *phone = customElements[@"phone"] NSString *address = customElements[@"address"]; NSString *displayurl = customElements[@"displayurl"]; // To Get clickUrl NSString *clickUrl = customElements[@"link"][@"url"]; //To Get clickFallbackUrl NSString *clickFallbackUrl = customElements[@"link"][@"fallback_url"] }``` |
| Privacy URL | No | Yes | `response.privacyLink;` |
| Video | No | Yes | `response.vastXML;` |
| Custom | Yes | No |  |
| Context | Yes | No |  |
| Full text | Yes | No |  |




## OpenRTB Native

OpenRTB Native refers to using the OpenRTB Native Asset specification in ANNativeAdRequest and ANNativeAdResponse classes, allowing for more flexible and standardized ad requests and responses.
For more information on OpenRTB Native 1.2 spec standards, see [OpenRTB Native Ads Specification.1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf). 
> [!NOTE]
> OpenRTB Native is not available for all members. Please work with your Account Manager or contact Support if you have any questions.

### ORTB in ANNativeAdRequest

To use OpenRTB Native, the app needs to specify OpenRTB Native assets in the ANNativeAdRequest using the openRTBAssets  variable. The contents of this var should be an OpenRTB Native request represented in dictionary, following the OpenRTB Native 1.2 request markup.

```

ANNativeAdRequest *nativeAdRequest = [[ANNativeAdRequest alloc] init];
nativeAdRequest.openRTBAssets = @{
  @"ver": @"1.2",
  @"assets": @[
    @{
      @"id": @1,
      @"required": @1,
      @"title": @{
        @"len": @300
      }            
    },
    @{
      @"id": @2,
      @"required": @1,
      @"img": @{
        @"type": @1,
        @"w": @250,
        @"h": @300                
      }            
    }  
  ]
};
```

### Code Sample Swift for Request

```

let nativeAdRequest = ANNativeAdRequest()
nativeAdRequest.openRTBAssets = [
  "ver": "1.2",
  "assets": [
    [
      "id": 1,
      "required": 1,
      "title": [
        "len": 300
      ]            
    ],
    [
      "id": 2,
      "required": 1,
      "img": [
        "type": 1,
        "w": 250,
        "h": 300                
      ]            
    ]  
  ]
]
```
> [!NOTE]
> The app does not need to specify the eventtrackers array. SDK automatically populates the eventtrackers array with the values it supports. Even if the app provides a value, it will be overridden by the SDK.

## ORTB in ANNativeAdResponse

ORTB in response corresponds to the raw ORTB Native JSON, which is exposed converted to dictionary to the app using the  openRTBNative variable in the ANNativeAdResponse class. Like the request, the response dictionary will follow the OpenRTB Native 1.2 response markup, see [OpenRTB Native Ads Specification.1.2](https://www.iab.com/wp-content/uploads/2018/03/OpenRTB-Native-Ads-Specification-Final-1.2.pdf) for details.

In addition to exposing the raw ORTB Native response in openRTBNative, the SDK also parses and makes available standard ORTB Native response assets (img, title, video, and data) using variables such as  title, body, callToAction, rating, iconImage, iconImageSize, mainImage, mainImageSize, sponsoredBy, additionalDescription, vastXML, privacyLink. The SDK also automatically handles impression, viewability, and click tracking.

> [!NOTE]
> The app should register the view in which the native ad is rendered with the SDK. SDK will handle impression, click, and viewability tracking. App will not receive eventtrackers, imptrackers, jstracker, or clicktrackers in the openRTBNative variable.

### Code Sample Objective C for response

```

- (void)adRequest:(nonnull ANNativeAdRequest *)request
        didReceiveResponse:(nonnull ANNativeAdResponse *)response {
    // Network code ANNativeAdNetworkCodeAppNexusORTB indicates the response is ORTB
    if (nativeAdResponse.networkCode == ANNativeAdNetworkCodeAppNexusORTB) {
        NSDictionary<NSString*, id> *ortbNativeResponse = nativeAdResponse.openRTBNative;

        // App has the option to either
        // 1. Use the parsed title, description, etc., which the SDK readily makes
        // available and dip into the ORTB Native response for non-parsed/custom values
        // OR
        // 2. Handle all the ORTB Native response response parsing in the app

        // Accessing title, description etc using the getters exposed in
        // NativeAdResponse class
        NSString *title = nativeAdResponse.title;
        NSString *description = nativeAdResponse.body;
        NSURL *imageUrl = nativeAdResponse.mainImageURL;
        CGSize imageSize = nativeAdResponse.mainImageSize;
        
        
        // Parsing ORTB Native resposnse JSON
        // Extract "assets" array
        NSArray *assetsArray = ortbNativeResponse[@"assets"];
        for (NSDictionary *asset in assetsArray) {

            NSInteger assetId = [asset[@"id"] integerValue];
            NSLog(@"Asset ID: %ld", assetId);
            
            // defining asset type by it's id
            if (assetId == 1) {
                // title
                NSDictionary *titleDict = asset[@"title"];
                NSString *text = titleDict[@"text"];
                NSLog("Ad title: %@", text);
            } else if (assetId == 2) {
                // image
                NSDictionary *imgDict = asset[@"img"];
                NSString *imageUrl = imgDict[@"url"];
                NSInteger imageType = imgDict[@"type"];
                if (type == 1) {
                    NSLog(@"Icon image URL: %@", imageUrl);
                } else if (type == 3) {
                    NSLog(@"Main image URL: %@", imageUrl);
                }
            }
        }
    }
}
```

### Code Sample Swift for response

```

func adRequest(_ request: ANNativeAdRequest, didReceive response: ANNativeAdResponse) {
    // Network code ANNativeAdNetworkCodeAppNexusORTB indicates the response is ORTB
    if nativeAdResponse.networkCode == .appNexusORTB {
        let ortbNativeResponse = nativeAdResponse.openRTBNative;

        // App has the option to either
        // 1. Use the parsed title, description, etc., which the SDK readily makes
        // available and dip into the ORTB Native response for non-parsed/custom values
        // OR
        // 2. Handle all the ORTB Native response response parsing in the app

        // Accessing title, description etc using the getters exposed in
        // NativeAdResponse class
        let title = nativeAdResponse.title;
        let description = nativeAdResponse.body;
        let imageUrl = nativeAdResponse.mainImageURL;
        let imageSize = nativeAdResponse.mainImageSize;
        
        
        // Parsing ORTB Native resposnse JSON
        // Extract "assets" array
        if let assetsArray = ortbNativeResponse?["assets"] as? [[String: Any]] {
            for asset in assetsArray {
                guard let assetId = asset[@"id"] as? Int else { continue }

                switch assetId {
                    case 1:
                        guard let titleDict = asset["title"] as? [String: Any],
                            let text = titleDict["text"] as? String
                        else { continue }
                        print("Ad title: \(text)")
                    case 2:
                        guard let imgDict = asset[@"img"] as? [String: Any],
                            let imageType = imgDict["type"] as? Int,
                            let imageUrl = imgDict["url"] as? String
                        else { continue }

                        switch imageType {
                            case 1:
                                print("Icon image URL: \(imageUrl)")
                            case 3:
                                print("Main image URL: \(imageUrl)")
                            default:
                                break
                        }

                    default:
                        break
                }
            }
        }
    }
}
```

### Example: ORTB Native response JSONObject structure 


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
  // remaining ortb native 1.2 response fields would be here; ie for link,privacy etc
  // if available
} 
```



## Related topics

- [Integrate with iOS](ios-sdk-integration.md)
- [Mediate with iOS](mediate-with-ios.md)
