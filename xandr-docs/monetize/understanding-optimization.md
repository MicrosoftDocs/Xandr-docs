---
title: Understanding Optimization
description: In this article, find information about what optimization is, how it works, and when to use optimization.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Understanding optimization

> [!IMPORTANT]
> This guide only applies to the legacy line item. If you are using the augmented line item (ALI), see [Optimization Guide - ALI](optimization-guide-ali.md).

The Microsoft Advertising optimization engine is a tool that you can use to determine bid amounts based on campaign performance. This document will explain why optimization is beneficial to you, provide a high-level overview of the process of optimization, and tell you the information you can provide to Microsoft Advertising to make optimization as effective as possible. If you are unfamiliar with optimization, you should read this document before moving on to [Optimization In-Depth](optimization-in-depth.md).

## What is optimization?

Optimization at Microsoft Advertising is a tool that uses data to determine a bid that equals what an impression is worth to you (as a party making a bid). This algorithm calculates bids based on the performance of different pieces of inventory, bidding lower on inventory that generates fewer success events and higher on more valuable inventory. This is a highly efficient manner of bidding and allows you to get the greatest benefit for the money spent on campaigns.

If you're a network, rather than a direct trader, there's an additional layer of planning. Since optimization tries to bid an amount that is equal to the value of the impression (i.e., a break-even point) as determined by the network, networks often include a margin in their break-even point, so they can make a profit.

## How does optimization work?

If the advertiser is results-driven (i.e., wants clicks and/or conversions on their impressions), your campaign needs to obtain those success events as inexpensively as possible. Even if the advertiser is not results-driven, you still want to create a campaign that maximizes the number of impressions for the minimal price (so as to win their business in the future). In these instances, you would use optimization. To perform these tasks well, you must have information about the market and (in the instance of a results-driven advertiser) the dollar amount that the advertiser earns for each success event.

Once the campaign using optimization first begins, there is no data available on this campaign; therefore, we don't know how well it might perform. The optimization algorithm uses historical advertiser data to determine an initial bid. As the campaign wins more impressions and collects more data, optimization refines the bid further. It learns from the constantly-updated data. This is called the **Learn Phase**.

After a specified threshold of success events has been met, the optimization engine takes the campaign data and determines what it considers the optimum bid amount based on available knowledge (i.e., the amount that, when applied to the number of impressions required to obtain a success event, equals the value of the success event for the advertiser). This is called the **Optimized Phase**. Optimization continues to adjust the bid amount accordingly.

To understand the concept of optimization, assume that you are with 10 people in a room bidding on food, but you don't know anything about the inherent value of food. Each person has a finite amount of money, but wants the best meals available (based on flavor, nutrition, size, and variety). One dish is a hard-boiled egg, and another dish is a one-pound sirloin steak. If you didn't know the difference in the benefits of the steak compared to the egg, you wouldn't know how to bid on either item. You might bid $20 for the egg and $1 for the steak. Optimization would look at previous food auctions in other campaigns (as well as other foods bid on in this auction, if applicable) and tell you that the steak is much more valuable than the egg. You would therefore learn to bid a lower amount for the egg (so you don't waste your money) but to bid higher for the steak (so that you don't lose it to a higher bidder). Once you had purchased enough eggs and steaks, you would become confident that you can get the desired amount of each by bidding $5 per steak and $0.50 per egg. You won't win them all, but you'll win enough to satisfy your hunger.

The best way to illustrate optimization is to compare two campaigns - one that uses optimization and that does not use optimization.

- Campaign Beta is bidding a Base CPM of $2 (meaning it will bid that amount on all inventory), so it is not using optimization. Therefore, regardless of what that impression might be worth to the advertiser, the campaign bids $2 CPM. It wins some auctions and loses others; however, it often pays way too much for less valuable impressions (impressions with an RPM (Revenue Per Thousand) less than $2.00), thereby losing money, or bids too low on highly valuable impressions (impressions with an RPM (Revenue Per Thousand) greater than $2.00) and does not get those impressions.

- Campaign Alpha is going to use optimization and have it determine a bid based on a specifed CPA. It analyzes other campaigns from that advertiser to determine the rate of success events (clicks or conversions) and, in conjunction with the value that the advertiser assigns to a success event, determines a bid amount. As the campaign progresses, optimization adjusts the bid of Campaign Alpha based on the frequency of success events and the web page on which the inventory resides. Once it has enough data, optimization determines the bid amount that best meets the goals of the campaign and uses that amount (continuing to adjust the amount based on the web site). The campaign wins some auctions and loses others. Because optimization adjusted the bid amount based on the value of the inventory, this campaign spent appropriately for both higher-RPM and lower-RPM impressions.

## When should you use optimization?

There are certain situations where a network should use optimization in a campaign:

- If you are being paid on a CPC/CPA basis (since advertisers are paying the network when success events occur, you want to get the maximum number of success events for the lowest possible cost).
- If you are being paid on a cost plus basis (since advertisers are paying the network a fixed amount over the media cost, you want to have the lowest media cost possible).

Advertisers care about performance, even if they aren't paying you on a CPC/CPA basis (they still want their creatives to be seen by as many users in their target audience as possible, or to convert those impressions to success events). As a network, keeping your advertisers satisfied with the performance of their campaigns ensures repeat business. Therefore, it can be beneficial to use optimization simply to ensure maximized performance which you can demonstrate.

## How you can help

As with most processes, the results that optimization generates are only as good as the data that is fed in at the beginning. The more you know about how your success events are generated (also known as the conversion funnel), the better foundation that the optimization engine has to build upon. When we have more data, your campaign spends less time in the learn phase (and therefore spends less money to achieve its goals). This knowledge is obtained through the use of [Conversion Pixels](working-with-conversion-pixels.md) and [Segments](working-with-segments.md).

You should also consider the conversion path. These are the steps that a user takes from seeing a creative to clicking on it or performing the action suggested by the creative (e.g., making a purchase or signing up for a newsletter). Understanding this path is instrumental to ensuring advertising success. There are three main parts:

- Creative
- Landing page
- Conversion activity

### Creative

This is the ad that the user sees when the page is opened.

- The creative should attract the desired audience.
- The creative should clearly indicate what the user should do (e.g., Click **here** to download a song).
- The conversion should offer what the creative promoted (e.g., if the creative says to click here to sign up, the next step should be a sign-up page).

### Landing page

This is the URL that the user is sent to if they click on the creative. This can be considered a **success event**.

- The landing page should match the quality and appearance of the initial creative. Landing page quality can play a large role in conversion rate.
- It should be easy for users to locate the conversion and perform the required steps.
- Use conversion pixels liberally on your landing pages to provide multiple data points for optimization to analyze (this is especially important if there are many pages on your conversion path).

### Conversion

This is the action that you want the user to take based on the creative (e.g., buy something, provide an email address, etc.). This can be considered a **success event**.

- Ensure that the conversion is something that your audience will want to do (sign up for a newsletter, make a purchase online).
- In general, shorter conversion processes result in a higher conversion rate than long conversion processes (i.e., a ten-page form compared to a quick download). In some instances, longer conversion processes result in users returning to the site to complete the conversion at a later date.

## Audience and inventory targeting

It is important to choose to show your creatives to users who are most likely to respond positively to it (create a success event) by placing them on web sites that your desired users frequent.

### Audience

Audiences are segmented by their interests, which is determined by viewing the information associated to each user. The creative that you show an audience plays a large part is how successful your ad campaign will be. Are your creative and the offer it makes defined to reach the appropriate users? When you create the campaign, choosing the correct categories in which to serve the impression is critical. For example, you are going to have a very low success rate if your creatives for commercial electrical supplies are targeted to sites that cater primarily to pre-teens. When targeting, you should therefore should consider factors such as frequency of ad placement, age, gender, time of day, and day of week (e.g., users may be more likely to shop for certain services on weekends). This could involve retargeting ads to website visitors or finding a new audience through behavioral, contextual, or other targeting strategies.

### Inventory targeting

There is an abundance of inventory available on the internet, and it is neither cost effective nor possible to serve on all of it. Therefore, it is critical that you pick inventory your target audience would normally visit, and allow optimization to adjust the bid upward for those sites. Use the [Buy-Side Targeting](buy-side-targeting.md) options to narrow down your targeting in an informed way, thereby getting maximum benefit from each impression. This generally improves the speed and effect of optimization by directing resources away from inventory that will perform poorly. For example, if your offer involves signing up for local daily deals, advertising alongside global finance news may not be as effective as advertising on sites specializing in local entertainment, news, and reviews.

## Related topics

- [Optimization In-Depth](optimization-in-depth.md)
- [Prerequisite Knowledge](prerequisite-knowledge.md)
