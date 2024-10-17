---
title: Explore Publisher Ad Quality
description: Explore Publisher Ad Quality screen, highlighting network ad settings like Network Profile, Publisher Templates, and so on.
ms.date: 10/28/2023

---
# Explore publisher ad quality

The **Publisher Ad Quality** screen performs several functions:

- Allows you to view network-level ad quality settings such as your Network Profile or Publisher Templates

- Displays your Publisher Base and Conditional Rules. For each rule, the screen displays whether that rule is inheriting from a template
- Informs you of new brands as they are added to the platform

  This document describes the various sections of the **Publisher Ad Quality** screen and their functions.

## Navigation

Choose **Ad Quality** from the **Publishers** menu. Select the publisher from the dialog. Alternatively, from the **Publishers** screen, click on or hover over the publisher you want to work with. Select **Ad Quality** from the **Go to** menu for that publisher.

## Network profile

You can view your Network Profile settings here. To edit them, you'll need to go to the [Network Ad Quality Screen](network-ad-quality-screen.md). For more information, see [Update Your Network Profile](update-your-network-profile.md).

## Base and conditional rules

You can view and edit your Base and Conditional Rules here. If those rules inherit from a template, they will be marked as such. When a rule inherits from a template, it cannot be edited except by a network administrator. For more information, see [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md).

## Creative Approval

### Bidders

This feature is in "Closed Beta". Edit the trust levels associated with bidders and their buyer seats. To check which external DSPs are using Buyer Seat IDs see [External DSPs Using Buyer Seat IDs](./external-dsps-using-buyer-seat-ids.md).

### Review Creatives

**Review Creatives** tab you can search for creatives based on criteria such as who they're managed by or where they served. You can then approve or ban those creatives.

## Ad quality standards

This section is where you can determine which creatives serve on your inventory based on their creative attributes. You can also set frequency caps based on those attributes.

### Buyers

Edit the trust levels associated with individual buying members.

### Categories

Determine which categories of creative are eligible, e.g. "Airlines" or "Apparel."

### Technical attributes

Determine the eligibility of creatives based on technical attributes such as "Expandables" or "Flash."

### Brands

Allow or exclude creatives based on the brands they are associated with. You can apply a filter to see only new brands.

> [!NOTE]
> If an Ad Quality (AQ) is set as `default_brand_status:banned` but the parent brand is set as `status:trusted`, the child brand overrides the setting in `default_brand_status` and it will be able to serve unless it is explicitly banned in the Ad Profile's brand override list.

### Languages

Include or exclude creatives based on the language of the creative.

### Ad servers

Choose to serve only those creatives that are hosted on a specific set of ad server domains (see [Ad Server Settings](ad-server-settings.md) for more information on creating collections of eligible or banned ad servers). (Not available to all customers.)

### Frequency caps

Apply per-user frequency caps to creatives based on their technical attributes. You can also set frequency caps on creatives belonging to a sensitive category, e.g. "Alcoholic Beverages and References."

### Common searches

This section provides a convenient interface to some common search parameters, including:

- **Creatives that have served:** Search for creatives that have served on your network's inventory within a specified time period.
- **Creatives that have been uploaded:** Search for creatives of a specific brand status that have been uploaded within a specified time period.

### Advanced options

This section allows you to perform more complicated searches, including:

- **Creative ID or Media URL:** Search for a specific creative by its ID or URL. You can enter multiple comma-separated creative IDs.
- **Upload date:** Search for creatives uploaded within a specified time period.
- **Review Status:** Search for creatives with a specific review status. You can select multiple statuses.
- **Size:** Search for creatives of a specific size.
- **Creative format:** Search for creatives of a specific format. You can select multiple formats.
- **Media sub-type:** Search for creatives associated with a specific media sub-type. You can select multiple types.
- **Managed by:** Search for creatives by owner.
- **Brand:** Search for creatives associated with a specific brand. You can search for and select multiple brands.
- **Brand status:** Search for creatives by brand status. You can select multiple statuses.
- **Audit status:** Search for creatives by audit status. You can select multiple statuses.
- **Served on:** Search for creatives that have served on specific inventory within a specific time period.

  > [!NOTE]
  > Note that the "Served on" field defaults to "today." If you are searching for a creative that served before today, be sure to change this field to get results.

### Related topics

- [Working with Ad Quality](working-with-publisher-ad-quality.md)
- [Create a Custom Profile](create-a-custom-profile.md)
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
- [Network Ad Quality Screen](network-ad-quality-screen.md)
- [Update Your Network Profile](update-your-network-profile.md)
- [Create a Publisher Template](create-a-publisher-template.md)
- [Ad Quality Order of Operations](ad-quality-order-of-operations.md)
