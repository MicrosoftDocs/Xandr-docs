---
title: Pass Custom Keywords on iOS
description: This article provides information on passing custom keywords on iOS. Custom keywords are used to attach arbitrary key-value pairs to the request body of the ad call.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Pass custom keywords on iOS

Custom keywords are used to attach arbitrary key-value pairs to the request body of the ad call. These can be used for several purposes, including:

- Custom campaign targeting options (see [Key-Value Targeting](../digital-platform-api/custom-key-value-targeting.md) for more
 information)
- Reporting (see [Key Value Analytics Report](../digital-platform-api/key-value-analytics-report.md) for more information)

The following line of code adds a single key-value pair to the JSON body of ad the call:

```
// Add key foo with a single value (bar).
[banner addCustomKeywordWithKey:@"foo" value:@"bar"];
```

For a more robust/complex setup, you can pass multiple values for the same key in the ad call. To do this, call `addCustomKeywordWithKey:(NSString *)key value:(NString *)value `multiple times with the same key:

```
[banner addCustomKeywordWithKey:@"foo" value:@"bar"];
[banner addCustomKeywordWithKey:@"foo" value:@"baz"];
[banner addCustomKeywordWithKey:@"foo" value:@"foe"];
[banner addCustomKeywordWithKey:@"customkey" value:@"bar"];
```
