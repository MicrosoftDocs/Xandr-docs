---
title: OMID-Friendly Obstruction for iOS
description: The Open Measurement SDK enables third-party viewability and verification measurement for mobile ads without multiple SDKs. Publishers can get data on ad viewability.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# OMID friendly obstruction for iOS

The Open Measurement Software Development Kit (OM SDK) is designed to facilitate third party viewability and verification measurement for ads served to mobile app environments without requiring multiple Ad Verification Service Providers (Measurement Provider) SDKs.

Open Measurement Interface Definition (OMID) is an open measurement API provided by IAB. In short, it enables a publisher to get data on the viewability of an ad within a mobile device. For more detailed information about OMID, visit the IAB site [here](https://iabtechlab.com/standards/open-measurement-sdk/).

Friendly obstructions are the views that OMID will exclude from all viewability calculations when added to the OMID Session. When a UI element needs to be considered as a part of the ad, that can be added as a friendly obstruction to prevent it from counting towards coverage of the ad. For example, any native element such as a close button, some logo text, or other object that needs to be considered as a part of an ad (and not be counted for viewability measurement) should be registered as a friendly obstruction. This applies to any ancestor or peer views in the view hierarchy.

The OMID API enables:

- Adding a friendly obstruction
- Removing a friendly obstruction
- Removing all friendly obstructions

The details of these APIs for iOS platform for different AdUnits are discussed in the API details section.

In addition to the above mentioned functionalities, the OM SDK facilitates a property (`enableOMIDOptimization`) that enables optimization. Here, as part of optimization, viewability is tracked until an ad is fully visible to the user. Once the ad ceases to be
visible, viewability tracking stops. By default this property is set as `"NO"` and when set as `"YES"`, the OM SDK takes care of performing Open-Measurement Optimization.

## Properties

| Property | Type | Attribute | Description |
|:---|:---|:---|:---|
| `enableOMIDOptimization` | BOOL | readwrite | Indicates if Open-Measurement Optimization for viewability and verification measurement for ads served is enabled and if not, enable the same. Default value is `NO`.<br>***This API supports only banner and native ad types.*** |

```
/**
 If YES, the SDK will allow to perform Open-Measurement Optimization  for viewability and verification measurement for ads served. Default is NO.
 */
@property (nonatomic, readwrite) BOOL enableOMIDOptimization;
```

## Examples

### [Objective C](#tab/objectivec1)

```
ANSDKSettings.sharedInstance.enableOMIDOptimization = true;
```

### [Swift](#tab/swift1)

```
ANSDKSettings.sharedInstance().enableOMIDOptimization = true
```

## API details

### Adding a friendly obstruction

To add a friendly obstruction for Banner, Interstitial and Video AdUnits, you need to pass the view as an argument to the API.

### API for adding friendly obstruction

```
(void)addOpenMeasurementFriendlyObstruction:(nonable UIView *)obstructionView;
```

For Native AdUnits, you need to pass a friendly obstruction views list to add views as friendly obstruction with register view tracking.

### API for adding friendly obstruction

```
(BOOL)registerViewForTracking:(nonnull UIView *)view withRootViewController:(nonnull UIViewController *)rvc clickableViews:(nullable NSArray<UIView *> *)views openMeasurementFriendlyObstructions:(nonnull NSArray<UIView *> *)obstructionViews error:(NSError *__nullable*__nullable)error;
```

### Example for adding a friendly obstruction for AdUnits (Banner, Interstitial and Video)

```
[adObject addOpenMeasurementFriendlyObstruction:friendlyObstructionView]; 
```

### Example for adding a friendly obstruction for native AdUnits

```
[self.nativeResponse
    registerViewForTracking:self.nativeView
    withRootViewController:self clickableViews:@[]
    openMeasurementFriendlyObstructions:@[friendlyObstructionView1, friendlyObstructionView2, ...]
    error:nil];
```

## Removing a friendly obstruction

> [!NOTE]
> Native AdUnits does not support remove API. Friendly obstruction for Banner, Interstitial and Video AdUnits, you need to pass the view as an argument to the API.

### API for removing a friendly obstruction

```
(void)removeOpenMeasurementFriendlyObstruction:(nonable UIView*)obstructionView;
```

### Example for Removing a friendly obstruction for AdUnits (Banner, Interstitial and Video)

```
[adObject removeOpenMeasurementFriendlyObstruction:friendlyObstructionView];
```

## Removing all friendly obstructions

> [!NOTE]
> Native AdUnits does not support remove API.

### API for removing all friendly obstruction

```
(void)removeAllOpenMeasurementFriendlyObstructions;
```

### Example for removing all friendly obstruction for AdUnits (Banner, Interstitial and Video)

```
[adObject removeAllOpenMeasurementFriendlyObstructions];
```
