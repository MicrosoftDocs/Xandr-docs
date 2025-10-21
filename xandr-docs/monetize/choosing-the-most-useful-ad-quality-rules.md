---
title: Choosing the Most Useful Ad Quality Rules
description: Explore optimizing ad display with effective Ad Quality Rules. Adjust settings for technical attributes, content, language, buyer, and brand.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Choosing the most useful ad quality rules

Depending on the problems you're seeing, you can use different ad quality settings to include or exclude certain creatives on your site based on their technical attributes, content, language, buyer, or brand.

Here are some examples of how to find the right strategy to control ad display on your site:

| Ad Quality "Symptoms" | Strategy |
|--|--|
| I keep seeing ads from an undesirable domain on my site. | You can block domains associated with a brand using the **Brands** rules. For more information, see [Block a Brand Using Ad Quality Rules](block-a-brand-using-ad-quality-rules.md) |
| My users are complaining about too many ads for dating apps. | Use the **Frequency and Recency** settings to cap the number of times each user will see an ad in the Dating category per 12-hour period, or just use the **Categories** section to ban all content in the Dating category. |
| My consumers almost all speak French, and I only want to display ads in that language. | Use the **Language** settings to ban all languages, and then change the **Eligibility** setting for French to **Eligible**. |
| Interstitial ads don't conform to our site design. I want to make sure none of them can display on our inventory. | Use the **Technical Features** section to ban interstitial ads or other specialized kinds of ad technology. |
| Gambling ads are showing up and I want to block them. | Use the **Categories** section to search for Gambling. You can ban all gambling-related categories, or just specific ones like casino advertising. |
| A brand is competitive for one of my publishers, but not for all the publishers in the Network. | Create a publisher-level rule using the instructions provided in [Block a Brand Using Ad Quality Rules](block-a-brand-using-ad-quality-rules.md). |
| A certain buyer predictably serves ads that I find problematic. | Use the **Buyers** section to block that specific member from buying your inventory. |
| I only want a small selection of brands to serve on my inventory: do I have to ban all the other ones individually? | In the **Brands** section, change the **Default brand eligibility** to **Banned**. Then search for the brands that you do want to enable and change their **Eligibility** to **Eligible**. |

## Related topics

- [Improving Ad Quality on Your Inventory](improving-ad-quality-on-your-inventory.md)
- [Platform-Wide Banning](platform-wide-banning.md)
- [Block a Brand Using Ad Quality Rules](block-a-brand-using-ad-quality-rules.md)
