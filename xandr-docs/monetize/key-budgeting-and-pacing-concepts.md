---
title: Key Budgeting and Pacing Concepts
description: In this article, find information about the best ways to set up budgeting and pacing for your campaigns.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Key budgeting and pacing concepts

Budgeting and Pacing allows clients to determine the amount and frequency with which impressions are served. Of equal importance is how these features can keep clients from overspending or underspending their budgets. The information on this page will help you recognize and avoid the common errors associated with budgeting and pacing that lead to over- or underspend.

Even if you are using these features properly, it is still possible to create a situation where you either overspend your budget or serve your entire budget long before the end of the day or the end of the campaign.

## Test your conversion pixels

When working with budgets counting line item CPA, you should test your conversion pixels prior to the start of the campaign to ensure that all of your conversion pixels are firing properly. Without the count provided by the conversion pixels, there is no way to properly apply budgeting and pacing, since you cannot know when or how often clicks or success events are occurring.

> [!TIP]
> Go to **Advertisers**, and click on **Conversion Pixels** to see when the last conversion pixel fired.

## Proper budgeting

Unlimited budgets can allow the system to spend indiscriminately. Even though other safeguards may be in place, if you have not designated a budget amount, the campaign may continue to serve indefinitely. To be sure that there are no gaps through which an un-budgeted campaign could overspend, you should ensure that every campaign has a budget set either on the campaign level, on a line item or insertion order above it.

## Early campaign monitoring

One additional way to ensure that you stay within your budgeting parameters is to review the activity of your campaign to reach a small threshold; for example, observing how long it took to spend $50. Once you have this information over several intervals (e.g., at different times of the day), you can extrapolate the performance of the campaign and determine appropriate daily budget or pacing settings.

## Segment and geo targeting

Targeting by segment or geography allows you to restrict domains to which you will serve impressions based on user or location (geo). If you do not restrict your campaign to certain locations when that was your intention (e.g., you intend only to serve in certain states), or to certain user attributes (males age 17-35 who like fishing and drive pickup trucks) you can spend your entire budget well before the end of the day or the end of the flight (depending on whether you use **Lifetime Pacing** or **Daily Pacing**).

Conversely, if you are too restrictive in your targeting, you can limit the size of your segment to the point where you don't participate in enough auctions to spend your entire budget. Additionally, you may not win enough impressions to establish a valid pacing rate.

## Domain targeting

You can determine the domains you wish to serve on through the following methods:

- **Domain Lists**:
  
    Create one or more lists which can either include or exclude groups of domains and sub-domains. When applied to campaigns, these lists help determine the sites on which the campaign can serve impressions.

- **Campaign Targeting**:
  
    When creating a new campaign, you have access to targeting options that allow you to include or restrict certain geographic regions, demographics, segments, etc. These settings work in conjunction with Domain Lists to determine how impressions are served.

> [!NOTE]
> Refer to [Working with Targeting Lists](working-with-targeting-lists.md) for additional information on how these two features interact.

## Using the safety budget

> [!WARNING]
> Safety budgets are meant for CPM bidding and do not take CPA and CPC spending into account.

The safety budget acts as a limiting factor. It ensures that, regardless of the settings for a campaign, you cannot spend more than this dollar amount on third-party inventory per day. With the complexity of budgeting properly across geographic regions, bidder instances, time zones, and the inherent delay in receiving and acting upon auction data, many settings in a campaign (e.g., unlimited budget, no targeting, or no targeting by geography) can cause a severe budget overspend. The safety budget stops any campaign that reaches this limit; it is then restricted from bidding on any inventory.

It is recommended that you set this value to an amount that is 5-10 times your anticipated daily spend, but you should also take into consideration the amount of overspend that you can tolerate on any given day. When a campaign reaches 80% of the safety budget amount, emails are automatically sent to a client-specified list. It is recommended that the recipients of this email have the authority and knowledge to make changes to campaign details to avoid reaching the safety budget amount.

Refer to [Capping Daily Spend on Third-Party Inventory (Safety Budget)](capping-daily-spend-on-third-party-inventory-safety-budget.md) for more information about the safety budget.

## Budgeting with CPC or CPA revenue

When budgeting based on CPM or impressions, budget calculation is fairly simple. Each time a creative serves, the system recognizes the impression and counts it towards the budget. Even though there is a time-lag due to the speed and quantity of the bidding process (refer to [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)), this is usually relatively small because we are working in portions of seconds.

When working with clicks (CPC) or acquisitions (CPA) as success events, you can specify a **look back period**. This period defines the number of minutes, hours, or days that a success event can be claimed for your campaign after the user viewed or clicked on the creative. Refer to [Create a Conversion Pixel](create-a-conversion-pixel.md) for more information.

### Example

User Barbara is viewing a web page and sees a creative from your campaign for **travel2antarctica.com**. The **Post Click Interval** setting is **7 days**. She is interested and clicks on the ad, but does not provide her contact information (which is the defined success event); she does, however, bookmark the web page. Four days later, she returns to the web site and fills out a form to get promotional emails from that website. Because this success event falls within the **Post Click Interval** and was directly related to her viewing the creative from your campaign, that success event is attributed to your campaign.

The problem occurs when Barbara views the creative a few hours or minutes before the end of your campaign, but provides her information (the success event) four days later. The system has been budgeting and pacing exactly as you intended. However, using this example, you have now have a success event four days after the end of your campaign. Because there is no way the system can anticipate which impressions will resolve to success events after the end of the campaign, the system paces and budgets based on the actual campaign time frame. Assuming that your campaign hit its budget just as it ended, any success events like the example above cause overspend. The problem is exacerbated when you apply a higher value in the Post Click Interval or Post View Interval, and on campaigns with a high click-through rate.

## Resolving a CPC or CPA budgeting issue

While an exact resolution is difficult, there are steps you can take to minimize the overall impact of this issue.

- **Monitor your campaigns.** The more closely you pay attention to the rate at which impressions and success events are accruing, the sooner you can make adjustments to your budget, your pacing, or both.
- **Adjust your budget amount.** While this is not always possible, if you can determine an average percentage of impressions that lead to delayed success events, you can adjust your budget amount by that value near the end of the campaign.

## Related topics

- [Budgeting and Pacing](budgeting-and-pacing.md)
- [Why Use Budgeting?](why-use-budgeting.md)
- [Line Item Budgeting vs. Campaign Budgeting](line-item-budgeting-vs-campaign-budgeting.md)
- [Difficulties with Exact Budgeting](difficulties-with-exact-budgeting.md)
- [Daily Pacing](daily-pacing.md)
- [Line Item Pacing vs. Campaign Pacing](line-item-pacing-vs-campaign-pacing.md)
