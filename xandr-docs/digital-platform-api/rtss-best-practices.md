---
title: RTSS Best Practices
description: In this article, explore the best practices for the Real-Time Signals Service (RTSS).
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Real-Time Signals Service (RTSS) best practices

The following best practices will help you be successful using RTSS.

- [Real-Time Signals Service (RTSS) best practices](#real-time-signals-service-rtss-best-practices)
  - [API rate limits](#api-rate-limits)
  - [Segment naming](#segment-naming)
  - [Segment construction](#segment-construction)
  - [Target expiry](#target-expiry)
  - [OLC and geo-targeting](#olc-and-geo-targeting)
  - [Bulk uploads](#bulk-uploads)
  - [API retries](#api-retries)

## API rate limits

In order to prevent abuse of the API services, all accounts are generally limited to 10 read/writes per second. This limit is enforced programmatically by the API on a member level.

To avoid exceeding the rate limits, use the RTSS Bulk Upload service to upload multiple records. If the bulk upload file has more than 1 million records, wait 10-15 minutes before trying the next upload. For more information on API rate limits, see the [API Throttling](05---throttling-pagination-and-filtering.md) documentation.

## Segment naming

When you create segment objects for RTSS targets, it's a good idea to include `rtss` in the segment name, or to add this string as segment code. Labeling your RTSS segments makes it easier to identify which segments have RTSS real-time targets (IPs, OLCs, or lat/longs), as opposed to audiences (cookies/MAIDs). Clear naming also helps when troubleshooting segment objects.

For example, you could use the following naming convention:

rtss\_*kind_of_target(IP/OLC/Lat-Long)\_segmentName*

**Example**: A segment where you'll host OLC targets and want to name it myOLCsegment could be named `rtss_OLC_myOLCsegment`.

## Segment construction

For best results, don’t mix cookies and RTSS targets in the same segment--always keep them in separate segments. This separation makes future segment management and troubleshooting easier.

## Target expiry

When you upload targets to RTSS, make sure you keep track of their TTL. We assign a default expiry of 180 days per target unless otherwise specified. Keeping track of which targets will soon expire helps you avoid:

- Running campaigns failing to serve, because they’re targeting RTSS segments with expired targets.
- Uploading unnecessarily large files, instead of just the targets that will expire soon.

If you need to refresh your segments or create new ones frequently, the default 180 days is likely to be too long. For example, if you’re using OLC to target movement data from lat/long data, you might create a target that’s only valid for a short time. In this case, you should set a shorter TTL to avoid the resource costs of storing unused targets.

You can set TTL using `seg_ttl`, but this value includes processing time and may not be exact. The best practice is to use `expiry`, which sets the precise date and time when segments should expire. `expiry` is set at the file level, although segments whose explicit `seg_ttl` value would result in an earlier expiration than the expiry setting will still expire before the `expiry` date.

The following table shows the relationship between `seg_ttl` and `expiry` in the possible cases where one or both are specified.

| Scenario | Expiry Not Specified | Expiry Specified |
|:---|:---|:---|
| **TTL Not Specified** | Effective TTL = default TTL – processing_delay<br>For example, if the file is submitted on `3/1/2022 00:00:00` and processing starts the day after, then the effective TTL is `29` days and expiration occurs on `3/31 00:00:00`. | Effective TTL = specified expiry – (submission_time + processing delay)<br>For example, suppose the file is submitted on` 3/1/2022 00:00:00` with the explicit expiration date/time set to `4/1 00:00:00`. If processing starts on `3/2`, effective TTL is `30` days, and expiration occurs on `4/1`. |
| **TTL Specified** | Effective TTL = specified TTL – processing delay<br>For example, if the file is submitted on `3/1 00:00:00` with specified `seg_ttl` = `90` days, and processing starts the day after, then the effective TTL is `89` days and expiration occurs on `5/30 00:00:00`. | Effective TTL = explicit `expiry` or explicit `seg_ttl`, **whichever results in an earlier expiration**.<br>For example, suppose the file is submitted on `3/1` at `00:00:00`, with `expiry` set (on the file level) for `6/1` at `00:00:00`. If some records in the file do not include an explicit TTL, some have it set to `60` days, and some to `120` days, then, assuming processing starts right away, the effective TTL and expiration will be:<br>- Records without `seg_ttl` will have a TTL of `92` days and expire on `6/1`.<br>- Records with `seg_ttl = 120` will also have a TTL of `92` days and expire on `6/1`, because the expiry value results in an earlier expiration, and thus takes priority.<br>- Records with `seg_ttl = 60` will have an effective TTL of (`60` days - processing time) and an expiration date somewhere close to `5/1`. In this case, `seg_ttl` takes priority (but still be affected by processing time), because 60 < 90. |

## OLC and geo-targeting

RTSS uploads will accept any string that represents a valid OLC. By shortening the OLC code provided, you can specify a less precise area and increase your targeting zone. We recommend using a minimum of 4 symbols for OLC codes (an approximately 110km block, and a maximum of 8 symbols (an approximately 275m block)).

RTSS will use Lat/Long for location whenever it is provided at the time of impression, and will fall back to IP address otherwise. Lat/Long is usually only provided via in-app impressions, when the user has explicitly granted permission to the application to identify location of the device.

In most cases involving a desktop or mobile browser, the IP address is used to approximate location of the impression. IP Address precision is usually sufficient to identify to a zip code for desktop, but in some cases it can accurately identify a building, for example when an office has an explicit IP range. For mobile carrier connections, the IP Address will effectively give you the location of the cell tower that the device is connected to.

## Bulk uploads

To ensure good performance during bulk uploads:

- **Only upload deltas.** We recommend only uploading the changes in your data set to Xandr, rather than your entire data set. For example, if you have a file with 100,000 data points, but only 2000 of those rows have changed since last upload, only upload the 2000 rows of records that changed. This reduces upload time as well as the time required to process the data and make it available for targeting.
- **GZIP large files.** Use GZIP to compress your files to reduce upload times.
- **Use the correct file format.** Files should be saved in standard UTF-8 (without BOM) encoding. Use Unix-style line endings (line feed characters, not carriage returns), and make sure your file does not contain a trailing line ending.

## API retries

You may occasionally receive a `422: too many queries to the database` error from RTSS during periods of heavy load on our system. This occurs because RTSS prioritizes lookup requests from our bidders over API calls, so that segments are properly added on bid requests. We recommend building sleep/retry functionality into your process. If you do see a `422` error, have your process wait 3-5 seconds before trying again. Issuing an API call retry 1-2 times works in most cases.

If you see these errors frequently, you should also employ a random backoff on your API throttle.
