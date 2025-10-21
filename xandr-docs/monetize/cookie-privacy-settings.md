---
title: Microsoft Monetize - Cookie Privacy Settings
description: Manage Microsoft Advertising's cookie settings to control user data for segment targeting, frequency capping, and conversion attribution.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Cookie privacy settings

This document acts as an overview of the various cookie privacy-related settings that are available on the Microsoft Advertising platform. Below, you will find information about how to control use of cookie data on a given impression. For the purposes of this document, cookie data refers to information Microsoft Advertising stores on a user that is used for segment targeting, frequency capping, and conversion attribution.

Simple use cases for these settings include:

- If you typically want to use cookie data stored on users, but want the ability to not use cookie data when a user has expressed a desire to not be tracked:
  - Leave the `enable_cookie_tracking_default` parameter set to `true` on the [Publisher Service](../digital-platform-api/publisher-service.md) (this is the default setting).
  - For any users that do not wish to be tracked, include the `use_cookies=0` query string parameter as described in [Placement Tag Parameters](placement-tag-parameters.md) so no cookie data will be used or tracked for that user.
- If you only want to track or use cookie data on users that explicitly provide consent, you could:
  - Set the `enable_cookie_tracking_default` parameter set to `false` on the [Publisher Service](../digital-platform-api/publisher-service.md).
  - For any users that do provide consent, include the `use_cookies=1` query string parameter as described in [Placement Tag Parameters](placement-tag-parameters.md) so cookie data will be tracked for those users.
- For third-party creatives, you can have the hosting ad server determine whether to set cookies by using the `${USE_COOKIES`} macro as described in [Creative Macros](creative-macros.md).

For more information, see the linked documentation.

## Related topics

- [Placement Tag Parameters](placement-tag-parameters.md)
- [Creative Macros](creative-macros.md)
- [Publisher Service](../digital-platform-api/publisher-service.md)
