---
title: Add A Transition Animation on Android
description: In this article, learn how to add transition animations for banner ads on Android.
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# Add a transition animation on Android

The transition animation feature is disabled by default. To enable banner ad transition animations, implement the following code:

```
bav.setTransitionType(TransitionType.PUSH);
```

You can disable banner transitions by calling:

```
bav.setTransitionType(TransitionType.NONE);
```

The available transition types (including `NONE` to disable the feature) are:

- none
- random
- push
- reveal
- move in
- fade

In addition to its type, a transition animation has a direction and a duration (expressed in milliseconds) associated with it. Set the direction and duration of transition animations like so:

```
bav.setTransitionDirection(TransitionDirection.UP);  // or DOWN, LEFT, RIGHT
bav.setTransitionDuration( 1000 );
```

The default values for the direction and duration are `UP` and `1000`, respectively.
