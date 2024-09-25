---
title: Universal Pixel SDK for Android
description: This document is an overview on how publishers can integrate and install the Universal Pixel SDK (Pixie SDK) for Android.
ms.custom: android-sdk
ms.date: 10/28/2023
---


# Universal pixel SDK for Android

This document provides instructions on how publishers can integrate and install the Universal Pixel SDK (Pixie SDK) for Android.

## Integration instructions

**Requirements**

This SDK requires

- Android 4.0 or later
- Android SDK version 14 or higher

In order to use the Pixie SDK, you must have a valid Xandr Unified Pixel ID. This is an alphanumeric ID that represents a pixel in your app.

> [!NOTE]
> **Google Play**
>
>In order to enable the Android Advertising ID (AAID) , you must include Google Play Services as a dependency of your app. Xandr's SDK will still function without Google Play Services but will not produce the desired results.
>
> **Android Studio and Gradle**
>
> These instructions assume you are using Android Studio and Gradle. All of the required AndroidManifest.xml entries and ProGuard changes are automatically added to your app. If you are using other build systems, the steps may vary.

## Installation guide

Install via Maven from your `build.gradle` file as shown below. Note that the `[1,2)` notation means that when your app is compiled, the latest version of the SDK in the 1.x release series will be included. When we release a new version of the SDK, all you have to do to get the new version is recompile your app. Note that these are top-level blocks, not part of the buildscript block.

``` 
// Android: Gradle config to install the SDK
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-android-extensions'
repositories {
    maven{
        url "https://acdn.adnxs.com/mobile/pixiesdk/android/maven/"
    }
}
dependencies {
    implementation 'com.xandr.pixie:pixie-sdk:[1,2)'
    implementation("com.google.android.gms:play-services-ads-identifier:17.0.0")
}
```

## Implementation guide

## Initialization

Initialize the sdk as early as possible in the App's life cycle using the initialize() method, passing the pixel id and context as parameters.

``` 
Pixie.initialize(pixel_id: String, context: Context); 
```

## Track event

Once the SDK is initialized events can be tracked and submitted using **fireEvent()** method.  

> [!NOTE]
> Any events being tracked prior to initialization will be rejected.

``` 
Pixie.fireEvent(event: String, params: PixieParams, context: Context);
```

fireEvent() method takes Event string, PixieParams(optional) and Application context as parameters.

**event: String**

Standard Event strings are defined within the Event class. See below for the available Standard Event strings. You also have the option to define Custom Event string(s) in Universal Pixel UI and use it in your app.

Custom Event String(s) should be preregistered using Universal Pixel UI.

**params: PixieParams**

When tracking an event (both standard event and custom event), optionally you can also pass data associated with that event. Event data is represented by the PixieParams class. All parameters are optional.

| Name | Description |
|--|--|
| Properties |  |
| currency : String | Currency for the value specified. |
| itemId : String | A generic ID of the item represented. IDs can also be passed as an array of comma separated items. Example "itemId1, itemId2" |
| itemName : String | The name of the item represented. Names can also be passed as an array of comma separated items. Example "itemName1, itemName2" |
| itemType : String | A generic type of the item represented. Types can also be passed as an array of comma separated items. Example "itemType1, itemType2" |
| value : String | Value of a user performing this event to the business. |
| Function |  |
| put(key: String, value: String) | Arbitrary data defined by the publisher. Enables the passing of custom event data through key/value pairs. Keys should be preregistered using Universal Pixel UI. Values can be an array separated by a comma. |

**context: Context**

An application context

### Initialization code sample:

#### [Kotlin](#tab/kotlin1)

``` 
Pixie.initialize("2dad9dcd-de80-4dd1-b900-f4349082ab57",context)
```

#### [Java](#tab/java1)

``` 
Pixie.initialize("2dad9dcd-de80-4dd1-b900-f4349082ab57",context);
```

## Track standard event - page view

``` 
Event.PAGE_VIEW
```

The specific page that was visited. 

### [Kotlin](#tab/kotlin2)

``` 
Pixie.fireEvent(Event.PAGE_VIEW,context)
```

### [Java](#tab/java2)

``` 
Pixie.fireEvent(Event.PAGE_VIEW,context);
```

## Track landing page views

``` 
Event.LANDING_PAGE
```

Track landing pages' views.

### [Kotlin](#tab/kotlin3)

``` 
val landingPageParams = PixieParams(Value = "5.99", Currency = "USD", ItemId = "product_5,product_6", ItemName = "apparel,accessory", ItemType = "shirt,belt")
Pixie.fireEvent(Event.LANDING_PAGE,landingPageParams,context)
```

### [Java](#tab/java3)

``` 
PixieParams landingPageParams = new PixieParams("5.99","USD","product_5,product_6", "apparel,accessory","shirt,belt");
Pixie.fireEvent(Event.LANDING_PAGE,landingPageParams,context);
```

## Track key page views

``` 
Event.ITEM_VIEW
```

Track key page views (ex: product page, landing page, article).

## Code sample:

### [Kotlin](#tab/kotlin4)

``` 
val itemViewParams = PixieParams(Value = "5.99", Currency = "USD", ItemId = "product_5,product_6", ItemName = "apparel,accessory", ItemType = "shirt,belt")
Pixie.fireEvent(Event.ITEM_VIEW,itemViewParams,context)
```

### [Java](#tab/java4)

``` 
PixieParams itemViewParams = new PixieParams("5.99","USD","product_5,product_6", "apparel,accessory","shirt,belt");
Pixie.fireEvent(Event.ITEM_VIEW,itemViewParams,context);
```

## Track add to cart event

``` 
Event.ADD_TO_CART
```

Track when items are added to a shopping cart (ex: click, landing page
on Add to Cart button).


### [Kotlin](#tab/kotlin5)

``` 
val addToCartParams = PixieParams(Value = "5.99", Currency = "USD", ItemId = "product_5,product_6", ItemName = "apparel,accessory", ItemType = "shirt,belt")
Pixie.fireEvent(Event.ADD_TO_CART,addToCartParams,context)
```

### [Java](#tab/java5)

``` 
PixieParams addToCartParams = new PixieParams("5.99","USD","product_5,product_6", "apparel,accessory","shirt,belt");
Pixie.fireEvent(Event.ADD_TO_CART,addToCartParams,context); 
```

## Track checkout event

``` 
Event.INITIATE_CHECKOUT
```

Track when people enter the checkout flow (ex: click, landing page on checkout button).

### [Kotlin](#tab/kotlin6)

``` 
val initiateCheckOutParams = PixieParams(Value = "5.99", Currency = "USD", ItemId = "product_5,product_6", ItemName = "apparel,accessory", ItemType = "shirt,belt")
Pixie.fireEvent(Event.INITIATE_CHECKOUT,initiateCheckOutParams,context)
```

### [Java](#tab/java6)

``` 
PixieParams initiateCheckOutParams = new PixieParams("5.99","USD","product_5,product_6", "apparel,accessory","shirt,belt");
Pixie.fireEvent(Event.INITIATE_CHECKOUT,initiateCheckOutParams,context);
```

## Track add payment info

Event.ADD_PAYMENT_INFO

Track when payment information is added in the checkout flow (ex: click, landing page on billing info)

### [Kotlin](#tab/kotlin7)

``` 
val addPaymentInfo = PixieParams(Value = "5.99", Currency = "USD", ItemId = "product_5,product_6", ItemName = "apparel,accessory", ItemType = "shirt,belt")
Pixie.fireEvent(Event.ADD_PAYMENT_INFO,addPaymentInfoParams,context)
```

### [Java](#tab/java7)


``` 
PixieParams addPaymentInfoParams = new PixieParams("5.99","USD","product_5,product_6", "apparel,accessory","shirt,belt");
Pixie.fireEvent(Event.ADD_PAYMENT_INFO,addPaymentInfoParams,context);
```

## Track purchase event

``` 
Event.PURCHASE
```

Track purchases or checkout flow completions (ex: Landing on "Thank You" or confirmation page).

### [Kotlin](#tab/kotlin8)

``` 
let purchaseParams = PixieParams(value = "5.99", currency = "USD", itemId = "product_5,product_6", itemName = "apparel,accessory", itemType = "shirt,belt")
Pixie.fireEvent(Event.PURCHASE, eventParams:purchaseParams)
```

### [Java](#tab/java8)

``` 
PixieParams *purchaseParams = [[PixieParams alloc] initWithValue:@"5.99" currency:@"USD" itemId:@"product_5,product_6" itemType:@"apparel,accessory" itemName:@"shirt,belt"];
[Pixie fireEvent:Event.PURCHASE eventParams:purchaseParams]; 
```

## Track leads 

``` 
Event.LEAD
```

Track when someone expresses interest in your offering (ex: form submission, sign up for trial, registration).


### [Kotlin](#tab/kotlin9)

``` 
val leadParams = PixieParams(Value = "5.99", Currency = "USD")
Pixie.fireEvent(Event.LEAD,leadParams,context)
```

### [Java](#tab/java9)

``` 
PixieParams leadParams =  new PixieParams();
leadParams.setValue("5.99");
leadParams.setCurrency("USD");
Pixie.fireEvent(Event.LEAD,leadParams,context);
```

## Track custom event

Custom Events enable publishers to create their own events to track and submit. To create a custom event, initiate a PixelParams object with the data to be submitted and pass that object, along with a string identifier to the Pixie SDK fireEvent method. Custom event data can also be sent in key-value pairs by using the put method of the PixelParams object.


### [Kotlin](#tab/kotlin10)

``` 
val customPixieParams = PixieParams(Value = "5.99", Currency = "USD")
customPixieParams.put("name", "Form Submission")
customPixieParams.put("email", "user1@appnexus.com")
customPixieParams.put("type", "subscribe,newuser")
Pixie.fireEvent("TestCustomEvent", customPixieParams, context)
```

### [Java](#tab/java10)

``` 
PixieParams customPixieParams=new PixieParams();
leadParams.setValue("5.99");
leadParams.setCurrency("USD");
customPixieParams.put("name","Form Submission");
customPixieParams.put("email","user1@appnexus.com");
customPixieParams.put("type","subscribe,newuser");
Pixie.fireEvent("TestCustomEvent",customPixieParams,context)
```

## Enable logging

Pixie SDK comes with a debug mode feature that enables logging during development. This can be turned on by setting the debugMode variable to true.  All logging will be disabled in the release build.

``` 
$ adb shell setprop log.tag.PIXIE VERBOSE
```
