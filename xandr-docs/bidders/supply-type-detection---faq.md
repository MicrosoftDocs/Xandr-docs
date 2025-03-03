---
title: Supply Type Detection - FAQ
description: Learn FAQs on Supply Type Detection.  
ms.date: 11/24/2023
---


# Supply Type Detection - FAQ

> [!NOTE]
> On February 13, 2018, we made changes to how the supply type field is set on inventory. No action is required from buyers or sellers, but customers should be aware of the change.

Currently, supply type is a field that sellers set on placement groups to identify impressions as **Web**, **Mobile Web**, or **App (CTV, Mobile)**, and buyers can choose to target supply type in campaigns and line items. To reduce errors from sellers misclassifying or leaving the default, Xandr will now detect and set supply type implicitly on every impression. As a result, buyers will be able to more accurately target the inventory they want, and sellers will have one less operational task in managing their inventory. Buyers specifically targeting mobile web may also see a bump in reach as this is a commonly misclassified supply type.

## FAQs

### What technologies does Xandr use to detect supply type?

Xandr uses DeviceAtlas to determine whether an impression originated from a mobile device or desktop/laptop, and uses referrer URL and application ID data to distinguish "app" traffic from "web" and "mobile web".

### Will there be any changes to reporting, or will I continue to be able to leverage supply type as a filter and dimension?

There are no changes to reporting; you can continue to use the supply type filter and dimension.

### If I find errors, how do I report them?

Report any issues using our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

### How will Xandr supply type detection differ from the supply type I have set on my inventory?

The majority of inventory will be unaffected by this change. However, "mobile web" is the most commonly misclassified supply type that we see. We frequently see placement groups configured with supply type "web" where many impressions should be instead classified as "mobile web". 

As a result, we expect to see a minor decrease in the volume of "web" impressions and a commensurate increase in "mobile web". The "app" supply type is also occasionally misclassified; a small volume of "app" impressions with invalid or missing app IDs supply will be reclassified as "web" or "mobile web".

### What happens to the values I currently set on supply type?

As Xandr is now detecting supply type, any supply type designations made in our platform UI will be overridden by Xandr detection.

### Will the supply type setting be removed from the UI and API?

Yes, these settings will be removed from both the UI and API. The exact timeline for this change is TBD. Please refer to this page for updates.

### Will I be able to see how my inventory is classified in the UI and API?

Supply type is still available as a reporting filter & dimension in several reports.

However, supply type designations will be removed from the Placement Group and Placement summary screens in the UI and the `supply_type` field will be removed from the Site Service. The exact timeline for this change is TBD. Refer to this page for updates.

### What happens to line items and campaigns that are currently targeting supply type? Will they continue to work?

Yes, line items and campaigns will continue to work and no action is required from buyers to adjust them. Buyers targeting "mobile web" may observe a small increase in reach as this is a commonly misclassified supply type.

### Will inventory type targeting be available on my Guaranteed Delivery and Standard Line Items too?

Inventory type targeting is only available in Augmented Line Items. Supply type targeting can be used in Guaranteed Delivery and Standard Line Items to distinguish between web and app supply.

### Will this impact my inventory forecasts?

In the first few days following this release there may be minor effects on supply forecasting, as "mobile web" is a commonly misclassified supply type. Forecasts for "web" might decrease and "mobile web" might increase commensurately. However, no action needs to be taken as this will normalize after a few days.

### Will this impact my existing reservations and delivery for my Guaranteed Delivery line items?

We expect most Guaranteed Delivery Line Items to not be impacted at all. Some line items may be minimally impacted. In virtually all cases, line items that are either include or exclude-targeting currently-misclassified supply type impressions will continue to include or exclude that supply following this release.
