---
title: Feed Status Service
description: Use the Feed Status service to check when new reporting data is available via the network analytics feed.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Feed Status service

The Feed Status Service lets you check when new reporting data is available via the [Network Analytics Feed](./network-analytics-feed.md). New data becomes available when:

- New hours of reporting data become available
- Previous hours of reporting data have been updated. This is a rare event which will occur if we need to reprocess the data for a feed for a given hour.

> [!NOTE]
> - This service is not available for the [Clicktrackers Feed](./clicktrackers-feed.md).
> - For more detailed instructions on how to use this feed in your integration, see [Bulk Reporting Feeds](./bulk-reporting-feeds.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `https://api.appnexus.com/feed-status?type=network_analytics_feed` | Check the status of your Network Analytics Feed |

## JSON fields

This service returns only two fields in an array of objects:

| Field | Type | Description |
|:---|:---|:---|
| `hour` | timestamp | The date and hour of reporting data whose status you're interested in. |
| `last_run` | timestamp | When the reporting data for hour was last updated by our data pipeline. This is usually a few hours later than the value of `hour`. |

> [!NOTE]
> Timestamps are reported in the UTC timezone, so you'll need to manually translate the UTC time to your standard timezone.

## Example

This service returns the last 30 days of hourly data with a simple `GET` call as shown below. For instructions on how to use this information to integrate with your own reporting systems, see [Bulk Reporting Feeds](./bulk-reporting-feeds.md).

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/feed-status?type=network_analytics_feed'

{
    "response": {
        "status": "OK",
        "num_elements": 732,
        "start_element": 0,
        "hours": [
            {
                "hour": "2013-11-20 00:00:00",
                "last_run": "2013-11-20 03:10:55"
            },
            {
                "hour": "2013-11-20 01:00:00",
                "last_run": "2013-11-20 05:10:05"
            },
            ... many, many hours of data...
            {
                "hour": "2013-12-20 11:00:00",
                "last_run": "2013-12-20 13:55:50"
            }
        ]
    }
}
```

## Related topics

- [Bulk Reporting Feeds](./bulk-reporting-feeds.md)
- [Report Service](./report-service.md)
