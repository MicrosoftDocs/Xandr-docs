---
title : Microsoft Monetize - Frequency and Recency Examples
description : The article shows examples of frequency and recency where you can combine frequency and recency settings to provide an ideal user experience and minimize overexposure.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Frequency and recency examples

There may be instances where you want to combine frequency and recency settings to provide an ideal user experience and minimize overexposure.

For example, you want to ensure that a user can see a creative a maximum of 20 times in one month. However, you don't want them to see the creative 20 times in one day and then never again for the rest of the month, but instead you want to limit their exposure to a maximum of eight impressions per week. In this case, you would set the frequency cap to **20** impressions per **month** and **8** impressions per **week**.

Assuming we start at the beginning of the month, it's possible for the user to see the impression eight times the first week, eight times the second week, four times the third week, and then never again for the rest of that calendar month. This example assumes the user is seeing the impression the maximum number of times specified. Depending on your
targeting and the user activity, these numbers could be distributed differently. However, the maximums will not be exceeded.

You can combine these frequency settings with recency settings to further limit overexposure. In the preceding example, let's say you also set a recency cap of one impression every two hours. The user would still see a maximum of eight impressions per week, and all eight of those could be shown in the first day. However, with the impression
being shown only once every two hours, it will be at least 14 hours (starting from the time the first impression serves, which is considered hour 0) before the user has reached the maximum exposure of eight impressions for the week.

> [!NOTE]
> If you don't set a frequency cap, you can still set a recency cap. For example, you can set a recency cap of one impression every three days. With no frequency settings, each
> user can be shown an impression (at most) once every three days for the entire budget period.

## Additional frequency and recency examples

Here are some other examples that pertain specifically to frequency capping:

**Example 1**

You have a line item with four creatives attached: A, B, C, D. Each creative has a frequency cap of one impression per day, but the insertion order has no frequency limit. User Bill fits the line items's targeting parameters. He visits mysite.com and is shown creative A. Bill then visits coolsite.com and is shown creative D, then C, and finally B.
When more than one creative is eligible, any one of them could be shown randomly. At this point, there are no creatives left that meet frequency
eligibility and the line item does not serve to Bill again until the end of the 24-hour period.

In this case, you may want to set recency caps at the insertion order or line item level to prevent Bill from seeing creatives D, C, and B in one visit to coolsite.com. Setting recency caps will spread out the delivery of all creatives attached to this line item.

**Example 2**

Let's say each creative has a frequency cap of one impression per day, but the line item has a frequency cap of two impressions per day. Bill sees creative B and C (chosen at random) and the line item is maxed out until the 24-hour window resets.

**Example 3**

Bill fits the targeting for two line items (1 and 2). The line items share some of the same creatives.

> [!NOTE]
> Creative frequency applies to the creative universally across every line item or campaign that it is associated with.

Here are the frequency caps:

| Line Item 1 / CPM= $1 | Frequency=3 impressions per day |
|--|--|
| A | 1 impression per day |
| B | 1 impression per day |
| C | 1 impression per day |

| Line Item 2 / CPM=$2 | Frequency=1 impression per day |
|--|--|
| A | 1 impression per day |
| B | 1 impression per day |
| C | 1 impression per day |
| D | 1 impression per day |

If there are no other advertisers bidding on Bill, the first impression is won by LI 2, with its higher CPM. A creative is chosen at random, say Creative A. Now LI 2 and Creative A are maxed out. On the next impression, only LI 1 is eligible, and only Creatives B and C are still eligible (Creative A having already served). Creative B is served.

This can get far more complex as you add line items, creatives, and more nuanced frequency caps, such as "once per hour."

**Example 4**

Let's say you want to bid a CPM of $3 for the first time per day that a user sees a creative ($1 for viewings 2 - 4, and $0.50 for any further viewings). You can set up three identical line items with different CPMs and frequency caps as follows:

| Line Item 1 | $3 | CPM | 1 impression per day |
|--|--|--|--|
| Line Item 2 | $1 | CPM | 3 impressions per day |
| Line Item 3 | $0.50 | CPM | no limit |

On the first ad call, Line Item 1 will win the right to bid because it has the highest CPM. On the second ad call, Line Item 1 will not be eligible since it has reached its maximum frequency, so Line Item 2 will win the right to bid. On the fifth ad call, Line Item 2 will not be eligible, so Line Item 3 will win the right to bid.

## Related topics

- [Set a Frequency Cap](set-a-frequency-cap.md)
- [Set a Recency Cap](set-a-recency-cap.md)
