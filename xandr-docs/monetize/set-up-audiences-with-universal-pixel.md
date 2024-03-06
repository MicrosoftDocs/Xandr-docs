---
title: Microsoft Monetize - Set Up Audiences with Universal Pixel
description: Explore maximizing ads using a universal pixel. Effortlessly create audience segments, set rules, and optimize targeting in line items.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up audiences with universal pixel

You can set up audiences for your universal pixel using rules and conditions, then target the audience segments in the **Audience and Location Targeting** settings of your line item.

To configure an audience:

1. From the top menu bar, click **Advertisers** \> **Universal Pixel**.
1. Select a pixel from the **Universal Pixels** page.

   If no pixels are defined, use the setup instructions in [Universal Pixel Basic Implementation](universal-pixel-basic-implementation.md) to create one.

1. Click **+New**.
1. Provide a name for the audience.

   You can use this name to select an audience segment in your line item settings under **Audience Location and Targeting**.

1. Under **Include people who**, create conditions to define the audience segment you  want your pixel to populate. Use AND if you want all conditions to be fulfilled to qualify a user for the segment. Use OR if any of the conditions will qualify the user.
1. Under **Keep people in audience**, decide how long the users you have identified should remain in the audience segment you are creating.

   This number is sometimes called “Time to Live,” or TTL. The maximum TTL is 180 days. However, because cookies may become inactive, or users may no longer be relevant to the segment, we recommend a value of 60 days or less for most segments. For example, the users in a “highly motivated purchaser” segment may not remain highly motivated for a long duration.

1. Click **Save**.

   The audience segment will be displayed on the **Audiences** tab of the **Universal Pixels** page, and will be available for targeting by both name and segment ID in the **Audience and Location Targeting** settings of your line items.

   You can see audience segment activity updating on the **Audiences** tab as Microsoft Monetize collects data about your segments.

## Related topics

- [Set Up Conversions with Universal Pixel](set-up-conversions-with-universal-pixel.md)
- [Universal Pixel Rule Conditions](universal-pixel-rule-conditions.md)
- [Set Up Segment Targeting on a Line Item](set-up-segment-targeting-on-a-line-item.md)
