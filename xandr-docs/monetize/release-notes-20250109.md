---
title: January 09, 2025 - Prebid Server Premium Flexible Configurations
description: Explore the January 09, 2025 release, delving into PSP flexible configurations
ms.date: 01/09/2025
ms.topic: release-notes
ms.author: rupambaruah
---

# January 09, 2025 - Prebid Server Premium Flexible Configurations

Prebid Server Premium (PSP) flexible configurations allow sellers to package their Monetize SSP inventory for demand partners via targeting parameters (geographic location, device attribute, key value, etc.). Instead of creating a PSP configuration for each placement, a single configuration can be used to capture all inventory meeting targeting criteria — for example, all United States in-app inventory — to be sent to PSP demand partners. We expect this will reduce the number of configurations required within PSP, although your inventory structure in demand partners’ platforms may limit flexibility. For customers that prefer to use an API, a streamlined endpoint is available.

Documentation for the UI can be found [here](create-a-psp-configuration.md) while API changes are detailed on the [configuration service](../digital-platform-api/config-service.md) and new [campaign objects service](../digital-platform-api/campaign-object-service.md) pages.
