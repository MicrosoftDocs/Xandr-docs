---
title: Add a Transition Animation on iOS
description: In this article, learn how to add transition animations for banner ads on iOS.
ms.custom: ios-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# Add a transition animation on iOS

This page has instructions on how to add an animation to banner ad state transitions.

When ANBannerAdView presents more than one creative, a transition animation can be enabled between the visibly presented creative content.

By default, transitions are not animated. When there is no animation, one creative immediately replaces the other. Enable transition animations as follows:

```
bannerAdView.transitionType = ANBannerViewAdTransitionTypeFlip;
```

The enumerated type `ANBannerViewAdTransitionType` defines the possible transition types.

You can also define the duration and direction of the transition:

```
bannerAdView.transitionDuration = 2.5; // Duration in seconds.
bannerAdView.transitionDirection = ANBannerViewAdTransitionDirectionLeft;
```

The range of transition directions is defined by the enumerated type `ANBannerViewAdTransitionDirection`.
