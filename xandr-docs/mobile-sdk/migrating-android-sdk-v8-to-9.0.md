---
title: Migrating Android SDK v8 to 9.0
description: Publishers using SDK v9.0 must initialize Xandr SDK before making an ad request to avoid exceptions.
ms.custom: android-sdk
ms.date: 06/10/2024
ms.author: shsrinivasan
---

# Migrating Android SDK v8 to 9.0

Starting with SDK v9.0, we will no longer release source code updates for the Android/iOS Mobile SDKs on GitHub. Instead, all new SDK updates will be exclusively published on MavenCentral. Refer the installation guidelines for installing the SDK using Maven [Android SDK integration instructions](android-sdk-integration-instructions.md)

> [!NOTE]
> - Publishers who have integrated our SDK v8.11 or earlier using the source code method will need to migrate their integration to Maven.
> - There are no breaking changes while upgrading the SDK from 8.x to 9.0.