---
title: Frequently Asked Questions (FAQs)
description: In this article, explore about the Frequently Asked Questions (FAQs).
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Frequently Asked Questions (FAQs)

## Why are my third-party numbers different than first-party numbers?

There are several possible reasons for such a discrepancy:  

- Technological discrepancy - This occurs when the internet pipe "breaks" before the resulting ad is delivered (e.g., The connection is too slow and times out, or the user hits the back button or a new link before the ad has a chance to load). This causes a positive discrepancy.
- Accounting discrepancy - Because a huge percentage of internet traffic is not human, every vendor uses techniques to weed out and discount bot traffic. These techniques are not all the same. Therefore, what one vendor discounts as bot traffic, another counts as discrepancy. This discrepancy can be either positive or negative.
- Trafficking error - Complex ads can cause trafficking errors. An example of this is a tag with an embedded VAST tag in a flash ad, along with a non-flash static banner. This complexity can lead to cases where a single counted local event unintentionally sends multiple third-party event signals. This causes a negative discrepancy.
- Agency distributes the wrong tag - Sometimes, an agency sends two publishers the same exact tracker by accident. Both publishers are sending local impressions to that tag causing the third-party number to rise. When the publisher pulls the report from the third-party reporting system, ALL impressions from ALL sources are present in that report. So, the publisher may have only delivered 100k impressions to that DFA tag, but the report claims 2MM.
- Outside of view impressions - Sometimes, a publisher traffics a tag into a system to which Ad-Juster is not connected to (e.g., a newsletter email system). In these cases, third-party numbers are inflated.

## Related topic

[Ad Juster](ad-juster.md)
