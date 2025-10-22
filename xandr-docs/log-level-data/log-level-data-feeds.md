---
title: Log Level Data Feeds
description: In this article, learn about what Log level data feeds are, their use cases, and a list of all the log level feeds available.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Log level data feeds

> [!IMPORTANT]
> Log Level Data (LLD) feeds are not available via the API.

Log Level Data (LLD) feeds contain event-level data that enables you to build custom reporting and conduct in-depth analysis. Typically, log level data is used for reporting on dimensions not available in the Xandr UI/API reports. It can also be used for any analysis which requires event-level granularity, such as custom conversion attribution or identifying pools of high-value users.

**To subscribe to Log Level Data and learn about changes:**
If you are interested in receiving log level data feeds, talk to your Xandr representative about the data your use case will need, technical setup, and pricing.

## Overview

Log level data feeds include information about the following:

**Your managed publishers' transacted impressions**

This includes:

- Information about the impression sold (e.g., publisher ID, tag ID, and domain)
- Information about the user to whom the ad was served (e.g., user ID, geographic region, and user timezone)
- ID of the creative that served
  
**Your managed advertisers' transacted impressions, and any resulting clicks and conversions**

This includes:

- Information about the impression purchased such as advertiser ID, campaign ID, and creative ID
- Information about the user to whom the ad was served (e.g., user ID, geographic region, user timezone, and number of times the user has seen creatives from your advertiser)
- Information about the inventory where the impression served (e.g., Publisher ID or domain, if exposed by the seller)

**Segment pixel fires for all of your network's owned segments**

This includes network and advertiser level segments.

For a complete list of fields available to buyers and sellers, see the [List of log level Feeds](#list-of-log-level-feeds) section below.

> [!NOTE]
> **Timestamps**: If your log level data is provided in the *avro* format or one of the *protobuf* formats, the timestamp field values will be supplied in UNIX Epoch time.

## Use cases

Typical uses for log level data include:

- **Enhanced reporting** - report on additional dimensions such as geographic regions.
- **Segment management** -  build segments based on user actions and report on first-party data if your user IDs can be mapped to Xandr user IDs.
- **Conversion attribution** - see all actions leading to a conversion, experiment with custom conversion attribution.

## Data retrieval

Log level data may be obtained via batch files.

Use this method if data accuracy is paramount. Since batch files are relatively large, they cannot be consumed in the same way ordinary reports are. Clients who receive log level data will typically have their own engineering resources or a third-party vendor build an ETL process to load the data into their own database. Once in the database, the log- evel data can be used by their own reporting systems or data analysts.

See [Batch Log Level Data](batch-log-level-data.md) for more information on how to intake your data.

### Batch

| Features | Batch |
|---|---|
| Latency | over 1 hour |
| Viewability Information | ✓ |
| Failure recovery | ✓ |
| Export to Amazon S3 | ✓ |
| Data quality guaranteed | ✓ |

#### Recommended use cases

| Features | Batch |
|---|---|
| Financial calculations | ✓ |
| Real-time dashboards |  |
| Custom bidders |  |
| Campaign performance metrics | Final, long-term analytics |

LLD data is final and accurate. As a result, Batch LLD can be used to make financial calculations. If Xandr discovers an inconsistency, Batch LLD data will be reprocessed.

## List of log level feeds

The table below lists which feeds are available via LLD, the feed handle for each, and a link to view the feed columns.

| Feed | Feed Handle | Columns |
|---|---|---|
| Auction Categories Feed | `auction_category_feed` | [View](auction-categories-feed.md) |
| Bid Landscape Feed | `bid_landscape_feed` | [View](bid-landscape-feed.md) |
| Buyer Transparency Feed | `brand_transparency_feed` | [View](buyer-transparency-feed.md) |
| Conversion Pixel Feed | `pixel_feed` | [View](conversion-pixel-feed.md) |
| Curator Feed | `curator_feed` | [View](curator-feed.md) |
| Incrementality Feed | `incrementality_feed` | [View](../data-science-toolkit/log-level-incrementality-feed.md) |
| Key Value Auction Feed | `auction_kv_labels_feed` | [View](key-value-auction-feed.md) |
| Segment Feed | `segment_feed` | [View](segment-feed.md) |
| Standard Feed | `standard_feed` | [View](standard-feed.md) |
| Universal Pixel Feed | `universal_pixel_feed` | [View](universal-pixel-feed.md) |
| Video Event Feed | `video_events_feed` | [View](video-events-feed.md) |

Currently only available to Beta clients. Contact your Xandr representative for more information.

> [!NOTE]
> For **sample** files, see available downloads under the **Format and Schemas** section in [Batch Log Level Data](batch-log-level-data.md).
