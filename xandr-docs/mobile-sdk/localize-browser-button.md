---
title: Localize Browser Button
description: Explore how to localize the browser button with a detailed example.
ms.custom: android-sdk, ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Localize browser button

When using the SDK feature to open click-through links within an in-app browser (in a native iOS app), you might need to localize the "OK" button that is displayed in the browser. To perform this localization, use the **NSLocalizedString** macro.

Add a value for the "OK" key for the browser's OK button. For example, to localize to Finnish ad the following code to Localizable.strings(Finnish):

```
"OK" = "kunnossa";
```

The **NSLocalizedString** macro will fetch the localized string from the **Localizable.strings** file for the current localization.
