---
title: Pass Custom Keywords on iOS
description: Learn how to pass custom keywords on iOS to enable custom campaign targeting and reporting.
ms.custom: ios-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Pass custom keywords on iOS

Custom keywords are arbitrary key-value pairs attached to an ad request. They can be used for:

- Custom campaign targeting (see [Key-Value Targeting](../digital-platform-api/custom-key-value-targeting.md) for more information)
- Reporting (see [Key Value Analytics Report](../digital-platform-api/key-value-analytics-report.md))

## Methods

### Ad unit-level keywords

These keywords are scoped to a specific ad unit.

| Method | Description |
|:---|:---|
| `addCustomKeywordsWithKey:values:` | Adds one or more values for the given key. |
| `removeCustomKeywordWithKey:` | Removes all values associated with the given key. |
| `clearCustomKeywords` | Removes all custom keywords. |

> [!NOTE]
> `addCustomKeywordWithKey:value:` is deprecated. Use `addCustomKeywordsWithKey:values:` instead.

### Request-level keywords

These keywords are scoped to the overall ad request rather than a specific ad unit. When using `ANMultiAdRequest`, set request-level keywords directly on the `ANMultiAdRequest` object instead of on individual ad units.

| Method | Description |
|:---|:---|
| `addCustomKeywordsAtTopLevelWithKey:values:` | Adds one or more request-level values for the given key. |
| `removeCustomKeywordAtTopLevelWithKey:` | Removes all request-level values associated with the given key. |
| `clearCustomKeywordsAtTopLevel` | Removes all request-level custom keywords. |

> [!NOTE]
> `addCustomKeywordAtTopLevelWithKey:value:` is deprecated. Use `addCustomKeywordsAtTopLevelWithKey:values:` instead.

## Example

### Ad unit-level keywords

These keywords are scoped to a specific ad unit.

#### [Objective-C](#tab/objectivec1)

```objectivec
// Banner
ANBannerAdView *banner = [ANBannerAdView adViewWithFrame:rect placementId:@"123456" adSize:size];
[banner addCustomKeywordsWithKey:@"foo" values:@[@"bar"]]; // Add single value
[banner addCustomKeywordsWithKey:@"foo" values:@[@"bar", @"baz", @"foe"]]; // Add multiple values
[banner removeCustomKeywordWithKey:@"foo"]; // Remove a specific key
[banner clearCustomKeywords]; // Remove all custom keywords
// Native
ANNativeAdRequest *nativeAdRequest = [[ANNativeAdRequest alloc] init];
[nativeAdRequest addCustomKeywordsWithKey:@"foo" values:@[@"bar"]]; // Add single value
[nativeAdRequest addCustomKeywordsWithKey:@"foo" values:@[@"bar", @"baz", @"foe"]]; // Add multiple values
[nativeAdRequest removeCustomKeywordWithKey:@"foo"]; // Remove a specific key
[nativeAdRequest clearCustomKeywords]; // Remove all custom keywords
```

#### [Swift](#tab/swift1)

```swift
// Banner
let banner = ANBannerAdView(frame: rect, placementId: "123456", adSize: size)
banner.addCustomKeywords(withKey: "foo", values: ["bar"]) // Add single value
banner.addCustomKeywords(withKey: "foo", values: ["bar", "baz", "foe"]) // Add multiple values
banner.removeCustomKeyword(withKey: "foo") // Remove a specific key
banner.clearCustomKeywords() // Remove all custom keywords
// Native
let nativeAdRequest = ANNativeAdRequest()
nativeAdRequest.addCustomKeywords(withKey: "foo", values: ["bar"]) // Add single value
nativeAdRequest.addCustomKeywords(withKey: "foo", values: ["bar", "baz", "foe"]) // Add multiple values
nativeAdRequest.removeCustomKeyword(withKey: "foo") // Remove a specific key
nativeAdRequest.clearCustomKeywords() // Remove all custom keywords
```

---

## Request-level keywords

Use request-level keywords to attach targeting that applies to the overall ad request rather than a specific ad unit. When using `ANMultiAdRequest`, set these keywords directly on the `ANMultiAdRequest` object instead of on individual ad units.

> [!NOTE]
> For `ANMultiAdRequest`, keywords set on the `ANMultiAdRequest` object will override any request-level keywords set on individual ad units.

#### [Objective-C](#tab/objectivec2)

```objectivec
// Banner
[banner addCustomKeywordsAtTopLevelWithKey:@"foo" values:@[@"bar"]]; // Add single request-level value
[banner addCustomKeywordsAtTopLevelWithKey:@"foo" values:@[@"bar", @"baz", @"foe"]]; // Add multiple request-level values
[banner removeCustomKeywordAtTopLevelWithKey:@"foo"]; // Remove a specific key
[banner clearCustomKeywordsAtTopLevel]; // Remove all request-level keywords
// Native
[nativeAdRequest addCustomKeywordsAtTopLevelWithKey:@"foo" values:@[@"bar"]]; // Add single request-level value
[nativeAdRequest addCustomKeywordsAtTopLevelWithKey:@"foo" values:@[@"bar", @"baz", @"foe"]]; // Add multiple request-level values
[nativeAdRequest removeCustomKeywordAtTopLevelWithKey:@"foo"]; // Remove a specific key
[nativeAdRequest clearCustomKeywordsAtTopLevel]; // Remove all request-level keywords
```

#### [Swift](#tab/swift2)

```swift
// Banner
banner.addCustomKeywordsAtTopLevel(withKey: "foo", values: ["bar"]) // Add single request-level value
banner.addCustomKeywordsAtTopLevel(withKey: "foo", values: ["bar", "baz", "foe"]) // Add multiple request-level values
banner.removeCustomKeywordAtTopLevel(withKey: "foo") // Remove a specific key
banner.clearCustomKeywordsAtTopLevel() // Remove all request-level keywords
// Native
nativeAdRequest.addCustomKeywordsAtTopLevel(withKey: "foo", values: ["bar"]) // Add single request-level value
nativeAdRequest.addCustomKeywordsAtTopLevel(withKey: "foo", values: ["bar", "baz", "foe"]) // Add multiple request-level values
nativeAdRequest.removeCustomKeywordAtTopLevel(withKey: "foo") // Remove a specific key
nativeAdRequest.clearCustomKeywordsAtTopLevel() // Remove all request-level keywords
```

---
