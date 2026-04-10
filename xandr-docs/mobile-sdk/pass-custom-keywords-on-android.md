---
title: Pass Custom Keywords on Android
description: Learn how to pass custom keywords on Android to enable custom campaign targeting and reporting.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Pass custom keywords on Android

Custom keywords are arbitrary key-value pairs attached to an ad request. They can be used for:

- Custom campaign targeting (see [Key-Value Targeting](../digital-platform-api/custom-key-value-targeting.md) for more information)
- Reporting (see [Key Value Analytics Report](../digital-platform-api/key-value-analytics-report.md))

## Methods

### Ad unit-level keywords

These keywords are scoped to a specific ad unit.

| Method | Description |
|:---|:---|
| `public void addCustomKeywords(String key, String value)` | Adds a single value for the given key. |
| `public void addCustomKeywords(String key, ArrayList<String> values)` | Adds multiple values for the given key in a single call. |
| `public void removeCustomKeyword(String key)` | Removes all values associated with the given key. |
| `public void clearCustomKeywords()` | Removes all custom keywords. |

### Request-level keywords

These keywords are scoped to the overall ad request rather than a specific ad unit. When using `ANMultiAdRequest`, set request-level keywords directly on the `ANMultiAdRequest` object instead of on individual ad units.

| Method | Description |
|:---|:---|
| `public void addCustomKeywordsTopLevel(String key, String value)` | Adds a single request-level value for the given key. |
| `public void addCustomKeywordsTopLevel(String key, ArrayList<String> values)` | Adds multiple request-level values for the given key in a single call. |
| `public void removeCustomKeywordTopLevel(String key)` | Removes all request-level values associated with the given key. |
| `public void clearCustomKeywordsTopLevel()` | Removes all request-level custom keywords. |

## Example

### Ad unit-level keywords

These keywords are scoped to a specific ad unit.

#### [Java](#tab/java1)

```java
// Banner
BannerAdView banner = new BannerAdView(this);
banner.addCustomKeywords("foo", "bar"); // Add single value
banner.addCustomKeywords("foo", new ArrayList<>(Arrays.asList("bar", "baz", "foe"))); // Add multiple values
banner.removeCustomKeyword("foo"); // Remove a specific key
banner.clearCustomKeywords(); // Remove all custom keywords
// Native
NativeAdRequest nativeAdRequest = new NativeAdRequest(this, "123456");
nativeAdRequest.addCustomKeywords("foo", "bar"); // Add single value
nativeAdRequest.addCustomKeywords("foo", new ArrayList<>(Arrays.asList("bar", "baz", "foe"))); // Add multiple values
nativeAdRequest.removeCustomKeyword("foo"); // Remove a specific key
nativeAdRequest.clearCustomKeywords(); // Remove all custom keywords
```

#### [Kotlin](#tab/kotlin1)

```kotlin
// Banner
val banner = BannerAdView(this)
banner.addCustomKeywords("foo", "bar") // Add single value
banner.addCustomKeywords("foo", arrayListOf("bar", "baz", "foe")) // Add multiple values
banner.removeCustomKeyword("foo") // Remove a specific key
banner.clearCustomKeywords() // Remove all custom keywords
// Native
val nativeAdRequest = NativeAdRequest(this, "123456")
nativeAdRequest.addCustomKeywords("foo", "bar") // Add single value
nativeAdRequest.addCustomKeywords("foo", arrayListOf("bar", "baz", "foe")) // Add multiple values
nativeAdRequest.removeCustomKeyword("foo") // Remove a specific key
nativeAdRequest.clearCustomKeywords() // Remove all custom keywords
```

---

## Request-level keywords

Use request-level keywords to attach targeting that applies to the overall ad request rather than a specific ad unit. When using `ANMultiAdRequest`, set these keywords directly on the `ANMultiAdRequest` object instead of on individual ad units.

> [!NOTE]
> For `ANMultiAdRequest`, keywords set on the `ANMultiAdRequest` object will override any request-level keywords set on individual ad units.

#### [Java](#tab/java2)

```java
// Banner
banner.addCustomKeywordsTopLevel("foo", "bar"); // Add single request-level value
banner.addCustomKeywordsTopLevel("foo", new ArrayList<>(Arrays.asList("bar", "baz", "foe"))); // Add multiple request-level values
banner.removeCustomKeywordTopLevel("foo"); // Remove a specific key
banner.clearCustomKeywordsTopLevel(); // Remove all request-level keywords
// Native
nativeAdRequest.addCustomKeywordsTopLevel("foo", "bar"); // Add single request-level value
nativeAdRequest.addCustomKeywordsTopLevel("foo", new ArrayList<>(Arrays.asList("bar", "baz", "foe"))); // Add multiple request-level values
nativeAdRequest.removeCustomKeywordTopLevel("foo"); // Remove a specific key
nativeAdRequest.clearCustomKeywordsTopLevel(); // Remove all request-level keywords
```

#### [Kotlin](#tab/kotlin2)

```kotlin
// Banner
banner.addCustomKeywordsTopLevel("foo", "bar") // Add single request-level value
banner.addCustomKeywordsTopLevel("foo", arrayListOf("bar", "baz", "foe")) // Add multiple request-level values
banner.removeCustomKeywordTopLevel("foo") // Remove a specific key
banner.clearCustomKeywordsTopLevel() // Remove all request-level keywords
// Native
nativeAdRequest.addCustomKeywordsTopLevel("foo", "bar") // Add single request-level value
nativeAdRequest.addCustomKeywordsTopLevel("foo", arrayListOf("bar", "baz", "foe")) // Add multiple request-level values
nativeAdRequest.removeCustomKeywordTopLevel("foo") // Remove a specific key
nativeAdRequest.clearCustomKeywordsTopLevel() // Remove all request-level keywords
```

---
