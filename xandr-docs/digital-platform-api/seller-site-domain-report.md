---
title: Digital Platform API - Seller Site Domain Report
description: The Seller Site Domain report helps sellers understand inventory coming through publishers, optimize domains for campaigns, and understand audit impact.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Seller Site Domain report

The Seller Site Domain Report is designed to give sellers information about what kind of inventory is coming through a publisher. For example, as a seller, you might distribute placement tags to your publishers and then want to verify that those tags are running on the inventory you intended. In addition, this report allows you to:

- See what kind of inventory is coming through a publisher so you can understand how to value it
- Guarantee a certain degree of inventory quality to managed buyers
- Optimize on domains for managed campaigns
- Understand the business impact of Xandr audit and categorization

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- yesterday
- last_7_days
- last_30_days
- last_month
- month_to_date

> [!NOTE]
> None of the available time ranges will include today's data. The latest data will be from yesterday.
> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 60 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | time |  | `"2012-08-01"` | The month when an impression occurred on this placement. |
| `day` | time |  | `"2012-08-23"` | The day when an impression occurred on this placement. |
| `seller_member_id` | int | Yes | `2718` | The seller's Xandr member ID. |
| `seller_member_name` | string |  | `"MegaSeller"` | The seller's name. |
| `seller_member` | string |  | `"MegaSeller (2718)"` | **Deprecated** (as of October 17, 2016). |
| `content_category_id` | int | Yes | `23` | The ID of the universal content category associated with the audited domain. |
| `content_category_name` | string |  | `"Entertainment"` | The name of the universal content category associated with the audited domain. |
| `content_category` | string |  | `"Entertainment (23)"` | **Deprecated** (as of October 17, 2016). |
| `site_id` | int | Yes | `223936` | The ID of the [site](./site-service.md) containing this placement. |
| `site_name` | string |  | `"Total-Web Email"` | The name of the [site](./site-service.md) where the impression occurred. |
| `site` | string |  | `"Total-Web Email (223936)"` | **Deprecated** (as of October 17, 2016). |
| `site_domain` | string | Yes | `"gwar-rules-forever.org"` | The domain where the impression occurred.<br><br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed.<br><br>**Note**: In some cases, this field will be populated with a domain that is different than where the impression actually occurred, such as an ad server domain. For more information about why this happens, see [Passing Domains Across IFrames](#passing-domains-across-iframes) below. |
| `placement_id` | int | Yes | `737099` | The ID of the placement where the impression occurred.<br><br>**Note**: `placement_id` of `0` may appear for 3rd-party impression trackers. For more information about impression trackers, see the [Impression Tracker Service](./impression-tracker-service.md). |
| `placement_name` | string |  | `"Webmail.com ROS 728x90"` | The name of the placement where the impression occurred. |
| `placement` | string |  | `"Webmail.com ROS 728x90 (737099)"` | **Deprecated** (as of October 17, 2016). |
| `publisher_id` | int | Yes | `44389` | The ID associated with the publisher on whose site the impression occurred. |
| `publisher_name` | string |  | `"LOL - US"` | The name of the publisher on whose site the impression occurred. |
| `publisher` | string |  | `"LOL - US (44389)"` | **Deprecated** (as of October 17, 2016). |
| `imp_type_id` | int | Yes | `6` | The ID for the type of impression. Possible values (associated types in parentheses):<br>`1` ("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `imp_type_name` | string |  | `"Resold"` | The name of the type of impression that occurred. For possible values and more information about each type, see `imp_type_id`. |
| `imp_type` | string |  | `"Resold (6)"` | **Deprecated** (as of October 17, 2016). |
| `audit_type_id` | int | Yes | `3` | The ID of the type of audit performed on the domain where the impression occurred. |
| `audit_type_name` | string |  | `"By AppNexus"` | The name of the type of audit performed on the domain where the impression occurred. Allowed values:<br> - `"By Seller"`: The domain was self-audited.<br> - `"By AppNexus"`: The domain was audited by Xandr.<br> - `"By Seller & AppNexus"`: The domain was audited by both the seller and Xandr.<br> - `"Unknown Audit Type"`: This usually means that the domain is unaudited. In some cases, this means that the domain was not auditable for technical reasons. |
| `audit_type` | string |  | `"By Seller (1)"` | **Deprecated** (as of October 17, 2016). |
| `exposed_for_resale_id` | int | Yes | `0` | An integer that denotes whether this inventory is exposed for resale. Allowed values:<br>`0` (False)<br>`1` (True) |
| `exposed_for_resale` | string |  | `"Not Exposed"` | Whether this inventory is exposed for resale. Allowed values:<br> - `"Exposed"`<br> - `"Not Exposed"` |
| `domains_exposed_id` | int | Yes | `1` | An integer that denotes whether this inventory's domains are exposed for targeting by buyers. Allowed values:<br> - `0` (False)<br> - `1` (True) |
| `domains_exposed` | string |  | `"Exposed"` | Whether this inventory's domains are exposed for targeting by buyers. Allowed values:<br> - `"Exposed"`<br> - `"Not exposed"` |
| `supply_type` | string | Yes | `mobile_web` | The seller-classified channel to denominate supply in terms of web, mobile-optimized web, and mobile app impressions. Possible values are <br> - `'web'` <br> - `'mobile_app'` <br> - `'mobile_web'` |
| `mobile_application_id` | string | Yes | `‘343200656’ (iOS) or ‘com.rovio.angrybirds’ (Android)` | A targetable Apple App Store ID, Google Play package name, or Windows application ID. |
| `mobile_application_name` | string | Yes | `Angry Birds` | The name of the mobile application as it appears in the Apple App and Google Play Stores. |
| `mobile_application` | string | No | `Angry Birds (com.rovio.angrybirds)` | **Deprecated** (as of October 17, 2016). |
| `fold_position_id` | int | Yes | `0` | The ID of the fold position, i.e. where on the page the placement is located.<br>Possible values for impressions:<br> - `0` = "unknown"<br> - `1` = "above"<br> - `2` = "below" |
| `fold_position` | string | Yes | `"Unknown"` | The fold position, i.e. where on the page the placement is located. For allowed values, see `fold_position_id`. |
| `age_bucket` | string | Yes | `"25-34"` | The bucket for the age of the user. See [Age Buckets](#age-bucket) below for possible values.<br><br>**Note**: For impressions older than 100 days, the `age_bucket` will be `"unknown"`. |
| `age_bucket_id` | string | No | `"3"` | The ID of the age bucket. See [Age Buckets](#age-bucket) below for possible values.<br><br>**Note**: For impressions older than than 100 days, the `age_bucket_id` will be `0`. |
| `gender` | string | Yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note**: For impressions older than 100 days, `gender` will be `"u"`. |
| `is_remarketing` | int | Yes | `0`, `1` | If `1`, the campaign is remarketing. If `0`, the campaign is not remarketing.<br><br>**Note**: For impressions older than 100 days, `is_remarketing` will be `-1`. |
| `imps_filtered_reason_id` | int | Yes | `"3"` | The numeric ID associated with the reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. See `imps_filtered_reason` below for more information. |
| `imps_filtered_reason` | string | Yes | `"Invalid Domain"` | The reason why the impression request was filtered out by Xandr's inventory quality controls and the auction was not held. Possible reasons are:<br> - `"Invalid Domain" (1)`<br> - `"Invalid IP" (2)`<br> - `"Suspected Domain Detection Tampering" (3, 4, 5)`<br> - `"Unknown" (6, 7)`<br> - `“White Ops: General IVT” (17)` - consists of traffic identified through routine means of filtration, executed through application of lists or with other standardized parameter checks.<br> - `“White Ops: Sophisticated IVT” (18)` - consists of more difficult to detect situations that require advanced analytics, multi-point corroboration/coordination, significant human intervention, etc., to analyze and identify.<br> - `"Valid Impression" (0)` is also a valid filtered request reason, but in that case, an auction was held and it was not filtered. |
| `operating_system_id` | int | Yes | `24` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-families-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_name` | string | Yes | `"Android 2.3.5 Gingerbread"` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-families-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_id` | int | Yes | `2` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-families-service.md) to look up which operating system versions are within a given operating system family. |
| `operating_system_family_name` | string | Yes | `"Android"` | The ID of the operating system of the device.<br> - Use [Operating System Family service](./operating-system-family-service.md) to obtain a list of operating system families.<br> - Use the [Operating System Extended service](./operating-system-families-service.md) to look up which operating system versions are within a given operating system family. |

## Passing Domains Across IFrames

Serving ads inside of iFrames is preferred by publishers for a number of reasons, to include:

- **Increased Security**: For security reasons, communication between iFrames serving from different domains is prohibited by the browser. This is known as the "Same Origin Policy". For more information, see the W3C's [Same Origin Policy](https://www.w3.org/Security/wiki/Same_Origin_Policy) page.

- **Page Load Speed**: Page load speed is guaranteed to be unaffected by advertisements inside iFrames because iFrames allow asynchronous loading of both page content and advertisements. This ensures that the user does not have to wait for the rest of the page to load in the event that serving an advertisement happens more slowly than expected.

For these and other reasons, some networks provide their publishers with an iFrame in which to display advertisements. If this iFrame delivers its contents from the network's domain and not the publisher's, it can lead to difficulties in determining the domain on which an impression actually occurred.

For example, a publisher is given a snippet of HTML code to put on their pages that includes an iFrame referencing a network's domain, `best-network.net`:

```
<!-- Publisher's Web Page >
<iframe src="http://best-network.net"> <!-- iFrame Referencing Network Domain >
    <script src="http://cooladexchange.net/tag?id=12345"></script> <!-- Ad Exchange Placement serving on Network Domain >
</iframe>
```

The iFrame is located on the publisher's web page, but it is serving its contents from the network's domain. Because the page and the iFrame are hosted on different domains, the security restrictions of the "Same Origin Policy" apply, and communication between the publisher's page and the network's iFrame is forbidden. Therefore the network is unable to determine the actual domain of the publisher's page. As a result, the network passes along its own domain as the referring URL to the placement.

### Age bucket

| Bucket ID | Bucket Name |
|:---|:---|
| `0` | `"unknown"` |
| `1` | `"13-17"` |
| `2` | `"18-24"` |
| `3` | `"25-34"` |
| `4` | `"35-44"` |
| `5` | `"45-54"` |
| `6` | `"55-64"` |
| `7` | `"65+"` |

## Metrics

| Column | Type | Example | Description |
|:---|:---|:---|:---|
| `imps` | int | `200942` | The number of impressions coming through this site or placement. |
| `clicks` | int | `1982` | The number of clicks coming through this site or placement. |
| `network_revenue` | money | `1876.595304` | The amount of network revenue coming through this site or placement. |
| `publisher_revenue` | money | `93.489302` | The amount of publisher revenue coming through this site or placement. |
| `imps_viewed` | int | `30,450` | The number of measured impressions that were viewable, per the IAB Viewability definition, which states that an impression is viewable if 50% of the pixels are in-view during 1 consecutive second. |
| `view_measured_imps` | int | `10,120` | The total number of impressions that were measured for viewability. |
| `view_rate` | double | `58%` | The percentage of impressions that were viewable out of the total number of impressions measured for viewability. (Viewed Imps / View Measured Imps) |
| `view_measurement_rate` | double | `45%` | The percentage of impressions measured for viewability out of the total number of impressions. (View Measured Imps / Imps) |
| `imps_filtered` | int | `2,024` | The total number of bid requests for which Xandr did not hold an auction due to inventory quality concerns. See `imps_filtered_reason_id` and `imps_filtered_reason` (under **Dimensions**) for a list of the possible reasons. |

## Example

### Create a JSON formatted report request

```
$ cat report-request.json

{
  "report": {
    "report_type": "seller_site_domain",
    "columns": [
      "seller_member_id",
      "seller_member_name",
      "placement_id",
      "publisher_id",
      "publisher_name",
      "imps",
      "imp_type_name",
      "audit_type_id",
      "audit_type_name",
      "site_name",
      "site_domain",
      "exposed_for_resale_id",
      "exposed_for_resale",
      "domains_exposed_id",
      "domains_exposed"
    ],
    "filters": [
      "seller_member_id",
      "audit_type_id"
    ],
    "report_interval": "last_7_days",
    "format": "csv"
  }
}
```

### `POST` the request to the report service

```
$ curl -b cookies -X POST -d @report-request.json "https://api.appnexus.com/report"

{
  "response": {
    
    "report_id": "8d3697d23c87e5bebd44370630162990",
    "status": "OK"
  }
}
```

### Download the report data directly to a file

The most common way to download reporting data involves using the `report_id` in a call the **report-download** service, which returns reporting data directly in the file format you specify. In the `curl` all below, we use the `-o` option to specify that the report be saved in a file named `huge-report.csv`. For more details, see the **Using cURL** section in [API Semantics](./api-semantics.md).

```
$ curl -b cookies -o huge-report.csv "https://api.appnexus.com/report-download?id=8d3697d23c87e5bebd44370630162990"
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.

### Retrieve the report data wrapped in JSON (optional)

You will almost always want to use the method described in *Download the report data directly to a file* above. However, if for some reason you prefer to receive the reporting data wrapped in a JSON response, you may pass the `report_id` to the [Report Service](./report-service.md) directly.

```
$ curl -b cookies "https://api.appnexus.com/report?id=8d3697d23c87e5bebd44370630162990"
```
