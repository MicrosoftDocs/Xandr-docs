---
title: Microsoft Monetize - Frequency and Recency Caps
description: Explore controlling creative exposure to users with frequency and recency caps, preventing overexposure by managing displays.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Frequency and recency caps

From the **Audience & Location Targeting** section, you can apply frequency and recency caps to your line item to prevent overexposure by limiting how many (frequency) and how often (recency) creatives are shown to a user. You can use the Creative Frequency and Recency Report to view how often and how frequently users are viewing a specific advertiser's creatives.

When a user is shown an ad multiple times over a short period, that user can begin to ignore the ad, reaching the point where they don't even see it anymore. Or they can see it too often that they're simply annoyed by it. For example, you might decide that after a user has seen the same creatives more than three times in a single day, it's not worth showing that creative to that user again. You may also price a line item or campaign higher if the user has seen it fewer than three times in a day and price it lower if the user has seen it more than three times.

> [!NOTE]
> Delivering a creative, the actual graphical advertisement, and displaying it to the user is sometimes referred to as "serving the creative." It can also be referred to as "showing an impression" or "serving an impression." An impression (or imp) is defined as a creative served to a single user at a single point in time.

Because frequency and recency both involve creatives, they're sometimes used interchangeably. However, it's important to understand the difference between frequency and recency. A frequency cap can be set to limit the number of times a creative can be shown to a given user. For example, a creative might be shown to a user a maximum of ten times in one week. Whereas a recency cap can be set to pace how often the user is shown the creative. For example, a creative might be shown to a user no more than once every four hours.

"Any creatives covered in the frequency or recency cap" refers to all creatives associated with the object where the cap is set (advertiser, insertion order, or line item) and all its children. For example, let's say we set a frequency or recency cap at the advertiser level, and that advertiser has ten line items with two creatives associated to each line item. An impression served can include any one of those 20 creatives, and that counts as a single impression against the frequency or recency cap.

## Related topics

- [Technical Limitations of Mobile Buying](technical-limitations-of-mobile-buying.md)
- [Creative Frequency and Recency Report](creative-frequency-and-recency-report.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)