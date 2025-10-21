---
title: Network Ad Quality Screen
description: Explore the Network Ad Quality screen, view Network Profile, Publisher Template, update ad quality settings, and get notified of new platform brands.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Network Ad quality screen

The **Network Ad Quality** screen performs several functions:

- Displays Network Profile settings
- Displays Publisher Templates. For each template, the screen displays how many publishers are using it
- Allows you to update network-level ad quality settings such as the Network Profile or any Publisher Templates
- Informs you of new brands as they are added to the platform

This document describes the various sections of the **Network Ad Quality** screen and their functions. For more information on how to create or update these settings, see [Update Your Network Profile](update-your-network-profile.md) or [Create a Publisher Template](create-a-publisher-template.md).

## Navigation

Click the **Network** tab at the top left of the screen. Choose **Ad Quality** from the menu that appears.

## Profiles and templates

This section lists the Network Profile and the Publisher Templates you've created if any. The column to the right of each Publisher Template shows how many publishers are using that template.

## Ad quality standards

This section is where you can determine which creatives serve on your inventory based on their creative attributes. You can also set frequency caps based on those attributes.

### Buyers

Edit the trust levels associated with individual buying members.

### Brands

Allow or exclude creatives based on the brands they are associated with. You can apply a filter to see only new brands.

### Categories

Determine which categories of creative are eligible (e.g., "Airlines" or "Apparel").

### Technical attributes

Determine the eligibility of creatives based on technical attributes (e.g., "Expandable" or "Flash").

### Languages

Include or exclude creatives based on the language of the creative.

### Ad servers

Choose to serve only those creatives that are hosted on a specific set of ad server domains. See [Ad Server Settings](ad-server-settings.md) for more information on creating collections of eligible or banned ad servers.

### Frequency caps

Apply per-user frequency caps to creatives based on their technical attributes. You can also set frequency caps on creatives belonging to a sensitive category (e.g., "Alcoholic Beverages and References").

### Review creatives

Under the **Review Creatives** tab, you can search for creatives based on criteria such as who they're managed by or where they served. You can then approve or ban those creatives.

### Basic search

The basic search options that appear in the Review Creatives tab provide a convenient interface to some common search parameters, including creatives that have served, brand status, and who manages the creative.

### Advanced options

The **Advanced Options** section allows you to perform more complicated searches, including:

- **Creative ID or Media URL:** Search for a specific creative by it's ID or URL. You can enter multiple comma-separated creative ID's.
- **Upload date:** Search for creatives uploaded within a specified time period.
- **Review Status:** Search for creatives with a specific review status. You can select multiple statuses.
- **Size:** Search for creatives of a specific size.
- **Creative format:** Search for creatives of a specific format. You can select multiple formats.
- **Media sub-type:** Search for creatives associated with a specific media sub-type. You can select multiple types.
- **Brand:** Search for creatives associated with a specific brand. You can search for and select multiple brands.
- **Audit status:** Search for creatives by audit status. You can select multiple statuses.
- **Served on:** Search for creatives that have served on specific inventory within a specific time period.

> [!NOTE]
> The "Served on" field defaults to "today." If you are searching for a creative that served before today, be sure to change this field to get results.

## Related topics

- [Working with Ad Quality](working-with-publisher-ad-quality.md)
- [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)
- [Update Your Network Profile](update-your-network-profile.md)
- [Create a Publisher Template](create-a-publisher-template.md)
- [Create a Custom Profile](create-a-custom-profile.md)
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md)
- [Ad Quality Order of Operations](ad-quality-order-of-operations.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
