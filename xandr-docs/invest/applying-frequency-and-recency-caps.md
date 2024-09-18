---
title: Microsoft Invest - Apply Frequency and Recency Caps
description: Apply frequency and recency caps at different levels with the most restrictive setting taking precedence. Caps apply according to the strictest settings available. 
ms.date: 10/28/2023
---

# Microsoft Invest - Apply frequency and recency caps

You can apply frequency and recency caps at the advertiser, insertion order, line item, and creative levels, or any combination of these levels. When using frequency targeting at multiple levels, the most restrictive setting always takes precedence.

When you set a frequency or recency cap for an object at one level, its child objects will inherit that cap, but it will be inherited by all child objects as a group. For example, if you set a frequency or recency cap of ten impressions per day at the advertiser level and have ten line items attached to that advertiser, one line item could potentially use all ten of the allotted impressions on one user. If you would like to spread the ten impressions out more evenly among your line items, you should also set a frequency or recency cap at the line item level.

The frequency and recency settings will be applied according to the strictest settings available. For example, imagine that you have two creatives, A and B, associated with the same line item. The frequency settings for creative A specify that it can only serve three times per day (where a day is defined as a calendar day). Creative B is set to only serve once per day. However, the line item settings specify a frequency cap of two impressions per day.

Since the strictest settings are applied, the line item frequency settings override those set at the creative level. Although creative A's settings dictate that it can serve three times per day, it will never serve more than the two times per day specified at the line item level.

If creative B serves its single allowed impression to the user before creative A can serve, creative A will only be allowed to serve once to that user.

## Related topics

- [Set a Frequency Cap](./set-a-frequency-cap.md)
- [Set a Recency Cap](./set-a-recency-cap.md)
