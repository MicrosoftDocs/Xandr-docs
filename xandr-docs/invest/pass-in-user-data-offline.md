---
title: Microsoft Invest - Pass in User Data Offline
description: Learn how to transfer your data from the ad server or data warehouse to the Server Side Cookie Store.
ms.date: 10/28/2023
---

# Microsoft Invest - Pass in user data offline

If you have data that lives in your ad server or data warehouse today, you can make it accessible to your Microsoft Advertising ad campaigns. In this section we describe the server-side integration that allows you to pass this data into our [Server Side Cookie Store](server-side-cookie-store.md).

## Use case

Let's say Prostarr Sportswear puts a pixel on every one of their pages so that if a user visits, whether by search engine, through a link, or by typing in a page directly, they can attach a user ID to that user's cookie. Then segments can be associated to this user ID, such as "purchased within last 2 weeks" or "viewed shoe model XJ12." Then Prostarr wants to show ads to the users in these segments by using Microsoft Invest.

But what if Prostarr has segment information that cannot be passed to Microsoft Advertising so easily? For example, let's say Prostarr creates an internal "Propensity to Buy" metric which rates users as low, medium, or high. Or let's say a user who made a purchase and was put into a "remarketing segment" returns a purchase and Prostarr makes an internal correction to that segment.

## User ID mapping

Before you can pass us data, there must be a mapping of the Microsoft Advertising user ID and your user ID so that we can attach the data to the right user and offer it for your future use. Please read about this process at [User ID Mapping](user-id-mapping-with-getuid-and-mapuid.md).

## Server-side data integration with Microsoft Advertising

Once ID mapping has taken place, you can pass Microsoft Advertising your offline segment data via our [Batch Segment Service](../digital-platform-api/batch-segment-service.md).
