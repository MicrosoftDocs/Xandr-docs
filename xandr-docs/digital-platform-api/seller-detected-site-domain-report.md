---
title: Digital Platform API - Seller Detected Site Domain Report
description: Use the Seller Detected Site Domain report to view details about actual domains being sold without affecting the auction itself.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Seller Detected Site Domain report

> [!NOTE]
> This report was deprecated in 2021.

The Seller Detected Site Domain report is designed to provide visibility into the actual domains that are being sold, and provide a tag or publisher level "health-check". Giving sellers visibility into the actual domains provides deeper insight into the inventory that is coming into their network. The detected domains, however, do not have any impact on the auction itself.

The report is best utilized as an investigation tool. That is, a seller runs the report for specific tags or publishers that they want to dig into further. The seller may know off-hand what they want to investigate; for example, it could be a new publisher that they've signed up. But, it would be very useful to give them an easy way to identify potential problems in tags or publishers.

In addition, sellers mostly cares about the tags or publishers that are giving them the most revenue - there may be a long tail that is not worth the time to investigate. So, a seller runs this report to see their best performing tags or publishers as well as whether a tag or publisher is problematic.

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- today
- yesterday
- last_7_days
- custom

> [!TIP]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 7 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `hour` | time | Yes | `"2010-02-01 06:00:00"` | The hour when an impression occurred on this placement. |
| `month` | time | Yes | `"2012-08-01"` | The month when an impression occurred on this placement. |
| `day` | time | Yes | `"2012-08-23"` | The day when an impression occurred on this placement. |
| `seller_member_id` | int | Yes | `2718` | The seller's Xandr member ID. |
| `seller_member_name` | string | No | `"MegaSeller"` | The seller's name. |
| `seller_member` | string | No | `"MegaSeller (2718)"` | The name and ID of the seller member. |
| `content_category_id` | int | Yes | `23` | The ID of the universal content category associated with this site or placement. |
| `content_category_name` | string | No | `"Entertainment"` | The name of the universal content category associated with this site or placement. |
| `content_category` | string | No | `"Entertainment (23)"` | The name and ID of the universal content category. |
| `site_id` | int | Yes | `223936` | The ID of the [site](./site-service.md) containing this placement. |
| `site_name` | string | No | `"Total-Web Email"` | The name of the [site](./site-service.md) where the impression occurred. |
| `site` | string | No | `"Total-Web Email (223936)`" | The name and ID of the site. |
| `site_domain` | string | Yes | `"gwar-rules-forever.org"` | The domain where the impression occurred.<br><br>There are two additional values that may appear in place of a domain, specifically: `"deals.unknown"` or `"managed.unknown"`. These mean that we didn't receive a valid domain as the referrer. For example, the domain may be blank or otherwise malformed.<br><br>**Note**: In some cases, this field will be populated with a domain that is different than where the impression actually occurred, such as an ad server domain. For more information about why this happens, see [Passing Domains Across IFrames](#passing-domains-across-iframes) below. |
| `auction_site_domain` | string | Yes | `"gwar-rules-forever.org"` | The domain of the auctioned site. |
| `site_domain_audit_status` | string | No | `"Audited"` | Specifies the audit status of the auctioned site domain. Permissible values are <br> - `Audited`<br> - `Blocklisted`<br> - `AdServer`<br> - `Unauditable`<br> - `Pending`<br> - `Unaudited`|
| `site_domain_audit_status_id` | int | Yes | `8` | The identifier for the audit status of the auctioned site domain. |
| `detected_site_domain` | string | Yes | `"cnn.com"` | The actual domains that are being sold and where the impression actually occurred. |
| `detected_site_domain_audit_status` | string | No | `"AdServer"` | Specifies the audit status of the detected site domain. Permissible values are <br> - `Audited`<br> - `Blocklisted`<br> - `AdServer`<br> - `Unauditable`<br> - `Pending`<br> - `Unaudited`|
| `detected_site_domain_audit_status_id` | int | Yes | `4` | The identifier for the audit status of the detected site domain. |
| `is_blocklisted` | boolean | Yes | `No` | Specifies if the impression is in a block-list. |
| `detected_top_domain` | boolean | Yes | `Yes` | Specifies if detected site domain is the highest level within the hierarchy of a domain name. |
| `placement_id` | int | Yes | `737099` | The ID of the placement where the impression occurred.<br><br>**Note**: `placement_id` of `0` may appear for 3rd-party impression trackers. For more information about impression trackers, see the [Impression Tracker Service](./impression-tracker-service.md). |
| `placement_name` | string | No | `"Webmail.com ROS 728x90"` | The name of the placement where the impression occurred. |
| `placement` | string | No | `"Webmail.com ROS 728x90 (737099)"` | The name and ID of the placement where the impression occurred. |
| `publisher_id` | int | Yes | `44389` | The ID associated with the publisher on whose site the impression occurred. |
| `publisher_name` | string | No | `"LOL - US"` | The name of the publisher on whose site the impression occurred. |
| `publisher` | string | No | `"LOL - US (44389)"` | The name and ID associated with the publisher. |
| `imp_type_id` | int | Yes | `6` | The ID for the type of impression. Possible values (associated types in parentheses):<br>`1` ("Blank"): No creative served.<br>`2` ("PSA"): A public service announcement served because there were no valid bids and no default creative was available.<br>`3` ("Default Error"): A default creative served due to a timeout issue.<br>`4` ("Default"): A default creative served because there were no valid bids.<br>`5` ("Kept"): Your advertiser's creative served on your publisher's site.<br>`6` ("Resold"): Your publisher's impression was sold to a third-party buyer.<br>`7` ("RTB"): Your advertiser's creative served on third-party inventory.<br>`8` ("PSA Error"): A public service announcement served due to a timeout issue or lack of a default creative.<br>`9` ("External Impression"): An impression from an impression tracker.<br>`10` ("External Click"): A click from a click tracker. |
| `imp_type_name` | string | No | `"Resold"` | The name of the type of impression that occurred. For possible values and more information about each type, see `imp_type_id`. |
| `imp_type` | string | No | `"Resold (6)"` | The name and ID of the type of impression that occurred. |
| `audit_type_id` | int | Yes | `3` | The ID of the type of audit performed on the domain where the impression occurred. |
| `audit_type_name` | string | No | `"By AppNexus"` | The name of the type of audit performed on the domain where the impression occurred. Allowed values:<br> - `"By Seller"`: The domain was self-audited.<br> - `"By AppNexus"`: The domain was audited by Xandr.<br> - `"By Seller & AppNexus"`: The domain was audited by both the seller and Xandr.<br> - `"Unknown Audit Type"`: This usually means that the domain is unaudited. In some cases, this means that the domain was not auditable for technical reasons. |
| `audit_type` | string | No | `"By Seller (1)"` | The name and ID of the type of audit performed on the domain where the impression occurred. |
| `exposed_for_resale_id` | int | Yes | `0` | An integer that denotes whether this inventory is exposed for resale. Allowed values:<br>`0` (False)<br>`1` (True) |
| `exposed_for_resale` | string | No | `"Not Exposed"` | Whether this inventory is exposed for resale. Allowed values:<br> - `Exposed`<br> - `Not Exposed` |
| `age_bucket` | string | Yes | `"25-34"` | The bucket for the age of the user. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than 100 days, the `age_bucket` will be `"unknown"`. |
| `age_bucket_id` | string | Yes | `"3"` | The ID of the age bucket. See [Age Buckets](#age-buckets) below for possible values.<br><br>**Note**: For impressions older than than 100 days, the `age_bucket_id` will be `0`. |
| `gender` | string | Yes | `"m"`, `"f"`, `"u"` | The gender of the user.<br><br>**Note**: For impressions older than than 100 days, the `gender` will be `"u"`. |
| `is_remarketing` | int | No | `0`, `1` | If `1`, the campaign is re-marketing. If `0`, the campaign is not re-marketing.<br><br>**Note**: For impressions older than 100 days, `is_remarketing` will be `-1`. |

## Passing domains across IFrames

Serving ads inside of iFrames is preferred by publishers for a number of reasons, to include:

- **Increased Security**: For security reasons, communication between iFrames serving from different domains is prohibited by the browser. This is known as the "Same Origin Policy". For more information, see the W3C's ["Same Origin Policy](https://www.w3.org/Security/wiki/Same_Origin_Policy) page.

- **Page Load Speed**: Page load speed is guaranteed to be unaffected by advertisements inside iFrames because iFrames allow asynchronous loading of both page content and advertisements. This ensures that the user does not have to wait for the rest of the page to load in the event that serving an advertisement happens more slowly than expected.

For these and other reasons, some networks provide their publishers with an iFrame in which to display advertisements. If this iFrame delivers its contents from the network's domain and not the publisher's, it can lead to difficulties in determining the domain on which an impression actually occurred.

For example, a publisher is given a snippet of HTML code to put on their pages that includes an iFrame referencing a network's domain, `best-network.net`:

```
<!-- Publisher's Web Page >
<iframe src="http://best-network.net"> <!-- iFrame Referencing Network Domain >
    <script src="http://cooladexchange.net/tag?id=12345"></script> <!-- Ad Exchange Placement serving on Network Domain >
</iframe>
```

The iFrame is located on the publisher's web page, but it is serving its contents from the network's domain. Because the page and the iFrame are hosted on different domains, the security restrictions of the "Same Origin Policy" apply, and communication between the publisher's page and the network's iFrame is forbidden. Therefore, the network is unable to determine the actual domain of the publisher's page. As a result, the network passes along its own domain as the referring URL to the placement.

### Age buckets

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

## Example

### Create a report request

```
$ cat report-request.json

{
  "report": {
    "report_type": "seller_detected_site_domain",
    "columns": [
      "seller_member_id",
      "seller_member_name",
      "placement_id",
      "publisher_id",
      "publisher_name",
      "imps",
      "detected_site_domain_audit_status",
      "detected_site_domain_audit_status_id",
      "site_name",
      "detected_site_domain",
      "detected_top_domain",
      "auction_site_domain",
      "placement_id",
      "is_blocklisted"
    ],
    "filters": [
      "seller_member_id",
      "detected_site_domain_audit_status"
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

The most common way to download reporting data involves using the `report_id` in a call the **report-download** service, which returns reporting data directly in the file format you specify. In the `curl` call below, we use the `-o` option to specify that the report be saved in a file named `huge-report.csv`. For more details, see the **Using cURL** section in [API Semantics](./api-semantics.md).

```
$ curl -b cookies -o huge-report.csv "https://api.appnexus.com/report-download?id=8d3697d23c87e5bebd44370630162990"
```

### Retrieve the report data wrapped in JSON (optional)

You will almost always want to use the method described in *Download the report data directly to a file* above. However, if for some reason you prefer to receive the reporting data wrapped in a JSON response, you may pass the `report_id` to the [Report Service](./report-service.md) directly.

```
$ curl -b cookies "https://api.appnexus.com/report?id=8d3697d23c87e5bebd44370630162990"
```
