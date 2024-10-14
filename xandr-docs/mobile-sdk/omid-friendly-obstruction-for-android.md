---
title: OMID Friendly Obstruction for Android
description: The Open Measurement SDK enables third-party viewability and verification measurement for mobile ads without multiple SDKs. It is an API provided by IAB.
ms.custom: android-sdk
ms.date: 10/28/2023
ms.author: shsrinivasan
---

# OMID friendly obstruction for Android

## Overview

The Open Measurement Software Development Kit (OM SDK) is designed to facilitate third party viewability and verification measurement for ads served to mobile app environments without requiring multiple Ad Verification Service Providers (Measurement Provider) SDKs.

Open Measurement Interface Definition (OMID) is an open measurement API provided by IAB. In short, it enables a publisher to get data on the viewability of an ad within a mobile device. For more detailed on OMID, visit the IAB site [here](https://iabtechlab.com/standards/open-measurement-sdk/).

The friendly obstructions are the views which OMID will exclude from all viewability calculations when added to the OMID Session. When there is a UI element which needs to be considered as a part of the ad, that can be added as friendly obstructions to prevent it from counting towards coverage of the ad. For example, any native elements such as a close button, some logo text, or other objects which need to be considered as a part of an ad (and not be counted for viewability measurement), should be registered as friendly obstructions. This applies to any ancestor or peer views in the view hierarchy.

The OMID API enables:

- Adding a friendly obstruction
- Removing a friendly obstruction
- Removing all friendly obstructions

The details of these APIs for Android platform for different AdUnits are discussed below:

## API details: Android

### Adding a friendly obstruction

To add a friendly obstruction for Banner, Interstitial and Video AdUnits, pass the view as an argument to the API.

#### API for adding friendly obstruction

```
public void addFriendlyObstruction(View view)
```

#### Example for adding a friendly obstruction for AdUnits (Banner, Interstitial, Video and Native)

```
//Banner
bav.addFriendlyObstruction(view);
//Interstitial
iav.addFriendlyObstruction(view);
//Video
videoAd.addFriendlyObstruction(view);
```

For Native AdUnits, pass the list of friendly obstruction views with register tracking.

#### Example for adding a friendly obstruction for native AdUnit

```
public static void registerTracking(final NativeAdResponse response, final View view, final NativeAdEventListener listener, final List<View> friendlyObstructionsList);
public static void registerTracking(final NativeAdResponse response, final View container, final List<View> views, final NativeAdEventListener listener, final List<View> friendlyObstructionsList)
```

### Removing a friendly obstruction

> [!NOTE]
> Native AdUnits does not support remove API.

To remove a friendly obstruction for Banner, Interstitial and Video AdUnits, pass the view as an argument to the API.

#### API for removing a friendly obstruction

```
public void removeFriendlyObstruction(View view)
```

#### Example for removing a friendly obstruction for AdUnits (Banner, Interstitial and Video)

```
//Banner
bav.removeFriendlyObstruction(view);
//Interstitial
iav.removeFriendlyObstruction(view);
//Video
videoAd.removeFriendlyObstruction(view);
```

### Removing all friendly obstructions

> [!NOTE]
> Native AdUnits does not support remove API.

#### API for removing all friendly obstruction

```
public void removeAllFriendlyObstructions()
```

#### Example for removing all friendly obstruction for AdUnits (Banner, Interstitial and Video)

```
//Banner
bav.removeAllFriendlyObstructions();
//Interstitial
iav.removeAllFriendlyObstructions();
//Video
videoAd.removeAllFriendlyObstructions();
```
