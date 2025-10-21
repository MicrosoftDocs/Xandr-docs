---
title: Automatic Archiving of Buy-Side Objects
description: Learn how campaigns are archived once they are identified as stale or unused. This page talks about do's and dont's of Archived campaigns.   
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Automatic archiving of Buy-Side objects

Microsoft Advertising automatically archives campaigns that have been identified as "stale" or unused. Archiving reduces the overhead of managing older campaigns and makes it easier to stay below [your object limits](viewing-your-object-limits.md). It also releases system resources that Microsoft Advertising can use to drive better results for your active campaigns.

> [!NOTE]
> This feature is only enabled for campaigns using the standard line item.

Archived campaigns can:

- Be viewed in Monetize and in Reporting
- Be clearly distinguished from active campaigns in both UI and API
- Be duplicated
- Be sorted by their **"archived"** status

Archived campaigns cannot:

- Serve
- Be edited
- Be counted against object limits

## Archiving criteria

A campaign is archived if:

- It has not served in 180 days
- It was created or last edited at least 180 days in the past
- It is not in flight
- It does not have a flight date scheduled in the future

## Action required by clients

**None.** Your stale objects are automatically archived. Archived objects appear in the UI and their status is prominently marked. In the API, you can sort them using a flag (see **Technical Notes** below for more detail).

## Preventing an object from being archived

To prevent a campaign from being archived, edit it to extend the last edit date. You can also set a flight date that occurs in the future.

## Technical notes for API clients

The following fields have been added to the [Campaign Service](../digital-platform-api/campaign-service.md):

- `is_archived` (boolean) - indicates whether the object has been archived
- `archived_on` (timestamp) - when the object was archived

The **only method allowed** on objects with `is_archived` set to `true` is `DELETE`.

## Related topics

- [Explore Campaigns](explore-campaigns.md)
- [View Campaign Details](view-campaign-details.md)
- [Viewing Your Object Limits](viewing-your-object-limits.md)
- [Create a Campaign](create-a-campaign.md)
