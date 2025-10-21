---
title: Test and Control Targeting
description: In this article, learn what Test and Control is, how it helps in targeting, and how to set it up.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Test and Control targeting

> [!IMPORTANT]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

Test and Control targeting, also known as A/B testing, allows you to randomly divide our user pool into groups to test how different campaign and creative strategies impact performance, delivery, and other success metrics you may have.

Here's how it works:

- First, create a test/control pattern, where you define up to 5 groups and set the percentage of the user pool for each group (all groups must total 100%).
- Then, for each campaign that you want to include in the test, target the relevant user group, based on your testing strategy.

This page explains how to use Test and Control targeting to compare campaign and creative strategies.

## What is Test and Control?

Attribution is one of the trickiest problems in online advertising. Let's say someone sees an ad and then converts. How responsible was the ad? Maybe the user would have signed up anyway due to word of mouth or past experience or a TV ad.

To figure out how much effect ads are having, we can, on request, randomly select some percentage of users (usually 3-10%) and assign them into the control category. Their cookies are marked so that they will ALWAYS be served control ads until they clear their cookies or we end the test/control process.

## How does Test and Control work?

In order to properly run an A/B test, you must ensure that users are segmented and isolated to see only the campaign and creative/landing page combination that they are supposed to see. Other than the variable you are testing, all campaign criteria should be the same. This isolates the variable you are testing.

## How to set up an A/B Test in Monetize?

### Testing patterns

In order to run an A/B test you need to set up a testing pattern. A testing pattern is a division of users into user groups.

Test and Control targeting, also known as A/B testing, allows you to randomly divide our user pool into groups to test how different campaign and creative strategies impact performance, delivery, and other success metrics you may have. In the Test/Control Group section, you can create patterns of test groups and select which test group the campaign should target.

You can create up to 5 user groups per testing pattern. You must then decide what percent of users you would like to place in each group and name the groups.

### Cookieless users

By default Microsoft Advertising will exclude cookieless users from the A/B test because you cannot track clicks or conversions for cookieless users, therefore you cannot test performance on them. You also have the option to put all cookieless users in your control group.

We separate cookieless users into their own bucket (bucket "`0`"), so that they do not interfere with A/B testing if you choose not to target them.

### User group

A user group is one of the groups from your testing pattern. Once you've created your testing pattern, you will assign a user group to a campaign that you are using for testing. Next, go ahead and create the other campaigns you will be using for testing

### Test and Control setup tips

One test pattern should be applied to one line item. All campaigns under that line item should be used for the A/B testing pattern. A user group is equivalent to a campaign. To easily create campaigns that are identical other than the variable that you are testing, you can use Campaign Targeting Templates.

## Reporting on A/B testing

In [Advertiser Reporting](advertiser-reporting.md), you can filter by "User Groups." You can then choose from all campaigns that have a user group associated to them. If you choose "User Groups" as a dimension, we will sort all campaigns based on the user group they are placed in, instead of by the testing pattern.

## Example: Avoiding incidental roadblocks

A largely unknown benefit to the Test and Control feature set is the ability to prevent users from seeing the same ads multiple times on the same page.

For instance, let's take a case where you have three ad banners: a 160x600, 300x250, and 728x90. The design on all three is nearly identical. The client has determined that saturating a user's page with several of these ads does not add any incremental benefit to their campaign in terms of the user's propensity to convert. Therefore, they have asked you to ensure that any given page loads a single banner.

Here are the simple steps to accomplish this:

1. Follow the steps for Create New Test/Control Pattern. Choose a group name to correspond to each of the three creatives and divide the percentage evenly among the three group names to add up to 100%.
1. You may use an existing grouping if it contains the split you require.
1. We do not support decimal values in the percentage fields, so if the number of creatives does not divide 100 into whole-number percentages (e.g. 4 creatives = 25% apiece, but 3 creatives = 33.33% apiece), you can round the percentages so that so that the sum of the percentages adds up to 100 (i.e. 33% + 33% + 34% = 100%).
1. Create one campaign per creative.
1. Assign each campaign to one of the groups.

> [!NOTE]
> This functionality will target each creative/campaign to a specific user group. That means, for example, that users that see the 300x250 in the above example will never see the 160x600 or 728x90.

## Related topic

[Create a Campaign](create-a-campaign.md) (Standard Line Item only)
