---
title: Getting Started with Key/Value Targeting
description: Explore diverse user targeting with Buy-Side options, geography, domain, and inventory. Customize using defined keys for precise targeting.
ms.date: 10/28/2023
---

# Getting started with key/value targeting

You have many different options for targeting users in your line items and campaigns. One quick scan of the topics under [Buy-Side Targeting](buy-side-targeting.md) will show you many of those options, including targeting based on geography, domain, and inventory type. You can also target by defining custom keys and values.

Key/value targeting allows you to take information you've collected and target your line items or campaigns to specific sets of users based on that information. The components of key/value targeting are, or course, keys and values:

- A key is a category. For example, your company may have information on the types of music users listen to, or the types of cars they drive: for example, `music_genre` and `car_type` could be custom keys.
- A value is a specific instance of the key. The `music_genre` key could have values such as rock, jazz, and classical. The `car_type` key could include sedan, coupe, and SUV.

You can define unique keys and corresponding values that will be part of your targeting profile. Whether you use the UI or the API, key/value targeting allows you to target users based on your own custom data. You can also run reports to evaluate the effectiveness of your key/value targeting in meeting your goals. We've provided the following resources to help you learn more about key/value targeting and how to make it work for you.

> [!NOTE]
> If you're currently using query strings with segments to implement key/value targeting, migrating to the profile key/value targeting described here will provide enhanced ease of use, more flexibility, and improved reporting.

## From the UI

This is typically the simplest way of setting up your key/value targeting. From the user interface you can define your keys and values, then include them in your targeting settings on your line items or campaigns. You can define individual settings and even do bulk uploads.

- [Pre-Defining Targeting Keys and Values](pre-defining-targeting-keys-and-values.md)  

  This page describes how to pre-define keys and values. Before you can target keys and values, you must pre-define the keys. These keys will be available to target against when you create your line items and campaigns. You can also pre-define values. The keys and values you pre-define will be stored together and available for targeting. You
  aren't required to pre-define values; you'll be able to target non-predefined values when you set up your targeting. Values that are pre-defined can be reused in targeting on multiple line items or campaigns, whereas values created at the time of targeting will need to be recreated for each targeting instance. Once a value is either
  pre-defined or saved as part of targeting, it will begin showing up in reporting. (See Reports below for more information on reporting requirements.)

- [Key/Value Targeting](key-value-targeting.md)

  After you've defined your keys and, optionally, your values, you can begin to target them from your line items or campaigns. This page will walk you through the process of creating expressions to narrow down your targeting to the specific segment of users you're looking for.

  > [!IMPORTANT]
  > To target a placement using Key/Value Targeting and generate accurate reporting on impression delivery, it is mandatory to define a specific Value for each Key in Microsoft Monetize. In Microsoft Invest, the line item needs to target the specific pre-defined values in [key/value targeting](key-value-targeting.md).

## From the API

Creating key/value targeting through the API allows you to programmatically set up profiles to target on your custom keys and values. The API also offers enhanced granularity in your targeting expressions. In the UI you can create expressions that are two levels deep; using the API your expressions can go to a depth of up to five levels.

- [Custom Key Value Targeting](../digital-platform-api/custom-key-value-targeting.md)
  
  A targeting expression can be something like this:

  ```
  I want to target all users who drive minivans, play tennis or golf, and live in New York. 
  ```

  When you break this down into an expression, it looks like this:

  ```
  (car=minivan) AND (sport=tennis OR sport=golf) AND (state=New York) 
  ```

  This page walks you through designing your expression and building it out using the services listed below. It also explains the "levels of depth" we mentioned earlier.

- [Targeting Key Service](../digital-platform-api/targeting-key-service.md): Use this service to define your keys.

- [Targeting Value Service](../digital-platform-api/targeting-value-service.md): Use this service to define your values.

- [Profile Service](../digital-platform-api/profile-service.md): Use this service to add the key/value targeting expressions to the profile associated with the line item or
  campaign on which you're targeting.

## Reporting

You can run reports to receive a consolidated look at how your line items and campaigns are performing based on the key/value targeting you've set up. Only impressions from items that meet the following criteria will be reported on:

- Key must be pre-defined.
- Value must be pre-defined OR value must be targeted by at least one line item or campaign.
- Value is not a numeric range (greater than or less than).
- Value does not include a wildcard.

The following reports are available:

- [Key Value Analytics Report](key-value-analytics-report.md)
- [Key Value Analytics Report](../digital-platform-api/key-value-analytics-report.md)  
  This is the same report as the preceding, but available from the API.

- [Key Value Auction Feed](../log-level-data/key-value-auction-feed.md)  
  This is the log-level data feed for key/value auctions. (Contact your representative or [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) for access to this feed).

## Tagging

Impressions with key/value targeting will serve and be reported only for those impressions that were logged by a placement tag containing the `kw_` prefix on the key name. For example, a placement tag containing `keyname=value1` will not serve and therefore not be logged, whereas a placement tag containing `kw_keyname=value1` will serve and be logged.
This applies to ad calls with the following tag types: /tt, /ttj, /fpt, /jpt, /pt, /ptv, /ssptv, /mtj, /map, and /mob.

> [!NOTE]
> When using [Microsoft Advertising's seller tag](../seller-tag/seller-tag.md) (AST), omit the `kw_` prefix. AST uses the keyword object in the body of the request, so the prefix is not needed.

A maximum of 100 key/value pairs can be defined per tag.

## Video overview

For an overview of working with key/value targeting, see [Key/value targeting](key-value-targeting.md).
