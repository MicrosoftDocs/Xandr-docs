---
title: Microsoft Monetize - Segment Modifier Testing Guidelines
description: In this page, learn about Technical Requirements, Analytical Requirements, recommendations and testing best practices for clients who plan to integrate with their campaigns.  
ms.date: 10/28/2023
---


# Microsoft Monetize - Segment modifier testing guidelines

This document outlines the technical requirements, recommendations, and testing best practices for clients who plan to integrate [Segment Modifier](segment-modifier.md) with their campaigns.

## Technical requirements

Clients wishing to use segment modifiers should be proficient with the tasks and concepts listed below:

- **Auction Mechanics**: Clients must understand the basics of auctioning in order to build a user model that doesn't undervalue users.
- **Batch Segment API**: Clients who are performing more robust integrations (requiring bulk feeds of segment data coming into Monetize) will benefit from a working knowledge of the [Batch Segment Service](../digital-platform-api/batch-segment-service.md). For clients who will be adding modifier values through pixel fires, please see Page Level Modifiers below.
- **Audience Creation**: Clients are responsible for creating their own audience segments for targeting, either through collection via segment pixel, or offline computation based on their own analysis.
- **Optimization**: For performance oriented campaigns, clients must understand how our V7 optimization algorithm works in order to avoid redundancies if their user model will be used in conjunction with our own. Microsoft Advertising optimization uses past advertiser performance against the same pixel/click goal, and performance data against our own inventory definition. Therefore, a modifier that attempts to take into account the domain:user combination will be fighting our own optimization.
- **Log Level Data**: Clients can use [Log Level Data Feeds](../log-level-data/log-level-data-feeds.md) to do low-level analytics on the performance of their model. Since Log Level Data includes the individual user IDs to which the modifier is being applied, analyzing the exact relationship between modifier values and overall lift will be much easier.

## Analytical requirements

One of the key elements of segment modifier is that the client is responsible for creating the optimization model. As a result, Microsoft Advertising won't have visibility into the exact science behind the model's performance. Additionally, due to restrictions in our user database, neither will Microsoft Advertising have visibility into the individual values behind each user. Therefore, the client must accept the bulk of the test analysis. This includes recurring, daily analytics of segment modifier performance; since the client created the model, the client should be able to analyze it.

Microsoft Advertising can measure lift on a high level or guide performance testing best practices.

## Testing best practices

The best way to test segment modifier (or any buying strategy) is to use the Test/Control method, also known as A/B testing.

Here are the recommendations for designing a test:

- **Test/Control Strategy**: Typically when designing an A/B test, clients tend towards 10/90 splits in user group targeting. This is usually because they're testing a creative versus PSA to measure true post view lift, since spending your client's money on a PSA isn't what most buyers are being paid to do. However, with segment modifier the approach should almost always be 50/50. If the client also wants to test performance against another buying strategy such as a base bid, they should use a 10/45/45 testing setup.
- **Measuring Lift:** Measuring lift can be difficult. Some performance metrics, such as eCPC when optimizing for a click, are fairly cut and dried. However, optimizing to a post-view conversion is more nebulous, since a user could have "viewed" a creative in the sense that it was served on the page, and then converted. But if the creative was out of the view of the user (e.g., below the fold and the user didn't scroll down to see it), the creative didn't truly incite the user to perform the action. Taking that into consideration, here are our recommendations for a testing approach based on performance goals:
  - Click: 50/50 split, Test/Control
  - Post Click: 10/45/45 Test/Control, with a performance goal on each campaign and a PSA on the 10 user group
  - Post View: 10/45/45 Test/Control, with a performance goal on each campaign and a PSA on the 10 user group

> [!NOTE]
> For the **Post Click** and **Post View** approaches, if the user is also targeting cookie-less users, they should set up a separate campaign targeting user group 101 with a click performance goal.

## Campaign recommendations

Campaign setup will have a big impact on the testing process. In V7 of optimization, ongoing performance of campaigns under a new advertiser impacts the learn bids of new campaigns. Therefore, suitable campaigns for testing should have the following attributes:

- **Ongoing Performance Campaigns:** Testing a brand new campaign can have an impact on understanding the true lift of a modifier, because we lack the historical context of a campaign's performance. Ideally, the campaign selected for the modifier test should have been ongoing for at least a month or more, so we can know going into the test what sort of performance metrics we should expect from the control campaign.
- **High Daily Budget:** A low daily budget can result in inconsistent data due to distribution of budget across user groups. In general, when using Test/Control against an audience the higher the daily budget the better. While a minimum daily spend of $250.00 should work, $500.00 is recommended.

## Sample application approaches

### Page-Level modifiers

Page-level modifiers are when a modifier value is piggybacked on a normal on-page segment call. For example, if an advertiser has a hypothesis that they should modify the bid depending on the shopping cart contents of an e-commerce site, they'll need to compute the relative value of expected revenue for the cart contents, then fire the segment call using the "**&other=**" query string parameter. Depending on whether or not the user is already present in the modifier segment, this will either create or update an entry in the modifier.

- **Advantages**: This requires the least amount of technical infrastructure of any of the deployments of Segment Modifier. Although it does require the pixel to have some computational logic, no additional work is required.
- **Disadvantages**: There is no visibility into the relationship between the modifiers of different users; you could modify every user in a set up by 1.5, which is redundant and will increase your media cost. Additionally, it requires that you compress a complex bid valuation model into an on-page script, which will slow page execution and will likely not be palatable to every advertiser.

## Batch segment API modifiers

This is the most common and also the best asynchronous method by which you can apply segment modifier. Clients can upload their modifier segment using the API's [Batch Segment Service](../digital-platform-api/batch-segment-service.md), and apply the modifier to their campaign.

- **Advantages:** Since the client will be computing their optimization data offline, they'll have a holistic understanding of their user valuation model. As a result, they'll be able to measure exact performance data in conjunction with [Log Level Data Feeds](../log-level-data/log-level-data-feeds.md). Additionally, they can leverage the [Batch Segment Service](../digital-platform-api/batch-segment-service.md)'s error reporting feature to know whether or not their user model has been uploaded properly (on-page pixel fires lack this advantage).
- **Disadvantages:** Unlike on-page pixels, we have volume restrictions on batch segment API uploads. If the [Batch Segment Service](../digital-platform-api/batch-segment-service.md) is used for unnecessarily frequent uploads, the client will likely be asked to move towards a data provider integration approach.

## Related topics

- [Segment Modifier](segment-modifier.md)
- [Batch Segment Service](../digital-platform-api/batch-segment-service.md)
- [Batch Segment Service - File Format](../bidders/initial-bss-account-setup.md)
