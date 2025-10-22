---
title: Bulk Reporting Feeds
description: in this article, find information on the different types of Bulk Reporting Feeds and how to retrieve them.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Bulk reporting feeds

Bulk Reporting Feeds allow you to synchronize large data sets from our system to your proprietary reporting system so all of your data is centrally located. Syncing our data makes it easier for you to take advantage of your own analytic tools, manage billing and payments, and provide custom reporting or dashboards to your advertisers and publishers across all of your data. You can automate pulling this data on a consistent basis to keep your data up to date.

Bulk Reporting Feeds are different than standard reports in that they allow you to efficiently pull more detailed data across all advertisers and publishers while ensuring that all data is current.

## Types of bulk reporting feeds

This section provides information on the various categories of bulk reporting feeds that are available on the platform.

### Network analytics feed

This bulk reporting feed offers you extensive data on your network's buy-side and sell-side performance.

For a list of available columns, go to [Network Analytics Feed](network-analytics-feed.md).

### Clicktrackers feed

You can use [Click Trackers](click-tracker-service.md) to track user clicks on creatives served by third-party ad servers (i.e., not served by Xandr). This reporting feed provides data on those external clicks.

- Each row returned is for a single click event.
- For a list of available columns, go to [Clicktrackers Feed](clicktrackers-feed.md).

## Retrieve a bulk reporting feed

Reporting Feeds were built so you could automatically pull updated data each hour or every day and dump that data into your data warehouse. There are three main steps to synchronizing Xandr's reporting data:

1. Use the [Report Service](report-service.md) to request a reporting feed for a specific hour or day. Note that the Report Service imposes several restrictions in order to limit the size of data and post processing time:
    - You cannot add filters or orderings.
    - `start_date` and `end_date` must be passed in and must be within 24 hours of each other.
    - `start_date` must be within the past 30 days.
1. Use the [Lookup Service](lookup-service.md) to reference data such as object names and codes. For most object types, the Bulk Reporting Feed returns IDs only. You can use the [Lookup Service](lookup-service.md) to map IDs to, for example, names, codes, descriptions, and statuses.
1. Watch for notifications of new data availability

See the [example](#example) below for a detailed walk-through of this procedure.

## Examples

### Request a network analytics reporting feed

You request a reporting feed using the [Report Service](report-service.md). Note that the Reporting Service imposes several restrictions on reporting feeds in order to limit the size of data and post processing time:

- You cannot add filters or orderings.
- `start_date` and `end_date` must be passed in and must be within 24 hours of each other.
- `start_date` must be within the past 30 days.

First, you create the JSON request for the `network_analytics` reporting feed.

> [!NOTE]
> `report_type` must be set to `"network_analytics_feed"`.

```
$ cat report_feed

{
 "report":
    {
    "report_type" : "network_analytics_feed",
    "columns":[
       "advertiser_currency",
       "advertiser_id",
       "booked_revenue_adv_curr",
       "buyer_member_id",
       "clicks",
       "creative_id",
       "geo_country",
       "imps",
       "imp_type",
       "insertion_order_id",
       "line_item_id",
       "media_cost",
       "media_type",
       "pixel_id",
       "placement_id",
       "post_click_convs",
       "post_view_convs",
       "ppm",
       "profit",
       "publisher_currency",
       "publisher_id",
       "pub_rule_id",
       "seller_member_id",
       "seller_type",
       "site_id",
       "size",
       "total_convs",
       "total_network_rpm",
       "total_publisher_rpm"
    ],
    "row_per":[
       "line_item_id",
       "advertiser_id",
       "buyer_type",
       "seller_type",
       "bid_type",
       "size",
       "geo_country",
       "content_category_id",
       "placement_id"
    ],
    "start_date": "2011-07-30 00:00:00",
    "end_date": "2011-07-31 00:00:00",
    "format": "csv"
  }
}

$ curl -b cookies -c cookies -X POST -d @report_feed 'https://api.appnexus.com/report'

{
   "response":{
      "status":"OK",
      "report_id": "91281567ba7b36ef66be08cc4e637c8f",
      "dbg_info": {
         ...
      }
   }
}
```

Once the report has been generated, you query the [Report Service](report-service.md) to get a URL that you use to download the report to a file.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=91281567ba7b36ef66be08cc4e637c8f'

{
   "response": {
      "status": "OK",
      "report": {
         ...
         "created_on": "2011-08-01 19:13:35",
         "data": null,
         "url": "report-download?id=91281567ba7b36ef66be08cc4e637c8f"
      },
      "execution_status": "ready"
      }
   }
}
```

You then make another `GET` call with the download URL. When specifying the file to save to, be sure to use the file extension of the format you specified in the initial `POST`. If you did not specify a `"format"` in your initial `POST`, the format is `"csv"` by default.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report-download?id=91281567ba7b36ef66be08cc4e637c8f' > /temp/report_download.csv
```

### Match IDs to object names and reference data

For most object types, the reporting feed returns IDs only. You can use [Lookup Service](lookup-service.md) to map IDs to, for example, names, codes, descriptions, and statuses.

### Ensure that your data is up-to-date

In order to synchronize data, you need to know when to load new hours or days of data into your local database. To make this easy, we provide a [Feed Status Service](feed-status-service.md) to notify you when new hours of reporting data become available or previous hours have been changed.

> [!NOTE]
> The [Feed Status Service](feed-status-service.md) only works with the [Network Analytics Feed](network-analytics-feed.md). It does not work with the [Clicktrackers Feed](clicktrackers-feed.md).

We recommend that you store a local record of when you last pulled an hour or day of reporting data. To do this, create a database table with the following schema:

| reporting_ymdh | last_synchronized |
|---|---|
| 2011-07-01 00:00:00 | 2011-07-01 01:23:13 |
| 2011-07-01 01:00:00 | 2011-07-01 02:19:54 |

*reporting_ymdh* is the hour (or day) or reporting data you have synchronized with your local database.

*last_synchronized* is the timestamp of the last time you pulled reporting data for *reporting_ymdh* into your local database. This field should be set using the `created_on` timestamp returned on the report response.

You can then compare which hours you have already pulled with the hours available via the [Feed Status Service](feed-status-service.md). (Again, note that this only works with the [Network Analytics Feed](network-analytics-feed.md).) You can also compare the time that you last pulled an hour or day of data to the `last_run` timestamp for that hour. If `last_run` is greater than the last time you synchronized that hour, then we have updated that hour of data and you should re-load it into your database.

#### Example

Assume you want to synchronize the previous day of data within 15 minutes of reporting data becoming available or changing. If you are synchronizing data for 2011-07-01 in EST timezone, you need to wait until hours 2011-07-01 05:00 to 2011-07-02 04:00 are available.

In this case, you should setup a process to poll the [Feed Status Service](feed-status-service.md) every 15 minutes to check if all hours from the previous day are available in reporting. You would make the following call:

```
> curl -b cookies -c cookies -X GET 'https://api.appnexus.com/feed-status?type=network_analytics_feed'
{
  "response": {
    "status": "OK",
    "num_elements": 44,
    "start_element": 0,
    "hours": [
      ...
      {
        "hour": "2011-07-01 05:00:00",
        "last_run": "2011-07-01 06:16:28"
      },
      {
        "hour": "2011-07-01 06:00:00",
        "last_run": "2011-07-01 07:14:36"
      },
      ...
    ]
    ...
}
```

The `hours` array contains a list of hours which are currently available in reporting for the last 5 days, along with the time that the we finished aggregating that hour of data. Occasionally, we need to correct hours of data which are already available in reporting. If this happens, the `last_run` timestamp will be updated for the changed hour of data.

On each response, your process needs to parse the JSON response and check if hours 2011-07-01 05:00 to 2011-07-02 04:00 are available. When all hours are returned, your process would request a Report Feed for the previous day, 2011-07-01 in this case. The response from the Reporting Service contains a `created_on` timestamp of when you ran your report:

```
{
  "response": {
    "status": "OK",
    "report": {
      ...
      "created_on": "2011-07-02 01:13:35",
      ...
    },
    ...
  }
}
```

You would record the `created_on` timestamp to your database as your *last_synchronized* time for 2011-07-01:

| reporting_ymd | last_synchronized |
|---|---|
| 2011-07-01 00:00:00 | 2011-07-02 01:13:35 |

## Related topics

- [Report Service](report-service.md)
- [Network Analytics Feed](network-analytics-feed.md)
- [Clicktrackers Feed](clicktrackers-feed.md)
