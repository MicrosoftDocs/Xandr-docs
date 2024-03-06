---
title: Microsoft Monetize - Report Throttling
description: Learn how report requests are throttled at both the member and user levels. This page explains about the different limits set on users and how they are applied.
ms.date: 10/28/2023
---


# Microsoft Monetize - Report throttling

In order to ensure that our systems operate as smoothly as possible for all users, report requests are throttled at both the member and user levels. The limits and how they are applied are described below.

## User limits

When a report is submitted by a user, a check is performed to see if the user has submitted 6 report requests in the past 15 minutes that are either in pending status or currently being processed. If that limit has been met, an error message is generated.

## Member limits

Each member is limited to 5 report requests being processed at the same time (including all users under that member). Any report requests submitted in excess of this limit are placed in a queue. Each member can have up to 100 report requests in the queue at a time. If the member exceeds this amount, they will receive a `LIMIT` on their next `POST`.

## Example

User- and member-level throttling/limits interact with each other. The following example attempts to demonstrate a typical scenario. Assume that User A and User B are associated with the same member. All members have a limit of 5 report requests being processed concurrently. We assume, for this example, that the following report requests are all submitted within a 15 minute time span:

| Report Request | User | Status |
|--|--|--|
| 1 | User A | Processing |
| 2 | User A | Processing |
| 3 | User B | Processing |
| 4 | User B | Processing |
| 5 | User B | Processing |
| 6 | User A | Enqueued |
| 7 | User A | Enqueued |
| 8 | User A | Enqueued |
| 8 | User A | Enqueued |
| 10 | User A | Error |

Report request \# 6 is placed in the queue, since there are already 5 report requests being processed for this member. For the same reason, requests \# 6-9 are also placed in the queue. Finally, we can see that request \# 10 causes an error to be generated, since User A has submitted their 7th report request within a 15 minute time span.

## Related topics

- [General Reporting Concepts](general-reporting-concepts.md)
- [Network Reporting](network-reporting.md)
- [Analytics Reporting](analytics-reporting.md)