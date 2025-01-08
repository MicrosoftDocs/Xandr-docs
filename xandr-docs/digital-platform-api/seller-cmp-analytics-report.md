---
title: Digital Platform API - Seller CMP Analytics Report
description: Analyze Seller CMP Analytics report for insights on IAB transparency and consent framework strings on ad requests to endpoints.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Seller CMP Analytics report

The Seller CMP (Consent Management Platform) Analytics Report provides insight into the number, validity, and content of the IAB Transparency & Consent Framework (IAB TCF) strings on seller ad requests to our endpoints. This report enables sellers to answer questions like:

- How many ad requests contained TCF strings encoded according to the TCF V1 and V2 specifications?
- How many ad requests contained TCF strings that were not encoded properly and therefore invalid or malformed?
- Is my CMP (Consent Management Platform) correctly passing permission information?

## Overview

This report does not prove or disprove compliance with any laws or regulations. The language "GDPR applied" for this report means applied TCF logic. We support the IAB TCF and this report enables sellers using the TCF to confirm that TCF signals are communicated properly.

For instructions on retrieving a report, see [Report Service](./report-service.md) or the [example](#example) below.

Sellers wishing to have all of their ad requests treated according to the IAB TCF standards and policies can force application of TCF logic by passing `'gdpr=1'` according to the [IAB OpenRTB Spec](https://iabtechlab.com/wp-content/uploads/2018/02/OpenRTB_Advisory_GDPR_2018-02.pdf). If the GDPR parameter is omitted but the request includes a TCF string according to the IAB OpenRTB specification, the auction will also apply TCF logic.

A high number of present but malformed strings for a given publisher usually means that the publisher's CMP is not creating or encoding the strings according to TCF specifications, and therefore are unreadable to vendors. Unreadable strings, because they do not provide clear signals to vendors, are treated as no permission for any vendor, and should be avoided.

For more information about the IAB TCF, refer to the following resources:

- [IAB Europe's TCF Policies](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/)
- [IAB Europe's TCF Governance](https://iabeurope.eu/tcf-governance/)
- [IAB Techlab TCF v1 and v2 Technical Spec & Implementation Guides](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework)
- [IAB Techlab TCF RTB Spec](https://iabtechlab.com/wp-content/uploads/2018/02/OpenRTB_Advisory_GDPR_2018-02.pdf)

## Time frame

The `report_interval` field in the JSON request can be set to one of the following:

- custom
- last_7_days
- month_to_date
- last_30_days

> [!NOTE]
> To run a report for a custom time frame, set the `start_date` and `end_date` fields in your report request. For more details about these fields, see [Report Service](./report-service.md).

### Data retention period

Data retention period for this report is 30 days.

## Dimensions

| Column | Type | Filter? | Example | Description |
|:---|:---|:---|:---|:---|
| `month` | date | Yes | `"2010-02"` | The month in which the impression occurred. |
| `day` | date | Yes | `"2010-02-01"` | The day on which the impression occurred. |
| `seller_member_id` | int | Yes | `456` | The ID of the selling member. |
| `publisher_id` | int | Yes | `555` | The ID of the publisher associated with the impression. |
| `publisher_name` | string | No | `"PublisherA"` | The name of the publisher associated with the impression. |
| `publisher` | string | No | `"PublisherA (555)"` | The name and ID of the publisher associated with the impression. |
| `call_type` | string | Yes | `"/openrtb2"` | The type of the ad call request. |
| `url` | string | Yes | `"itunes.apple.com/us/app/weather-crave/id324565014"` | The URL of the incoming impression. |

## Metrics

| Column | Type | Example | Formula | Description |
|:---|:---|:---|:---|:---|
| `ad_requests_gdpr_country` | int | `10000` | ad_requests_gdpr_country | The number of incoming ad requests for which the impression originated from a GDPR-implementing country/region, or the impression contained a consent string. |
| `ad_requests_gdpr_applied` | int | `970` | ad_requests_gdpr_applied | The number of incoming ad requests for which TCF logic was applied. We apply TCF logic if the IAB OpenRTB Specified flag `gdpr` is set to `1` or if the `gdpr` flag is omitted but the request includes a `gdpr_consent` field. If your digital properties intend to use TCF for all GDPR-covered inventory, this number should be close to `num_ad_requests_gdpr_country`. |
| `ad_requests_gdpr_applied_malformed_consent_string` | int | `876` | ad_requests_gdpr_applied_malformed_consent_string | The number of incoming ad requests for which GDPR is applied, and the consent string is non-blank but malformed. |
| `ad_requests_gdpr_applied_blank_consent_string` | int | `988` | ad_requests_gdpr_applied_blank_consent_string | The number of incoming ad requests for which GDPR is applied, and the consent string is blank. |
| `ad_requests_gdpr_applied_invalid_consent_string_seller_revenue` | int | `666` | ad_requests_gdpr_applied_invalid_consent_string_seller_revenue | The number of ad requests for which seller revenue attributed for the incoming impressions, GDPR is applied and the consent string is either blank or malformed. |
| `ad_requests_gdpr_applied_valid_consent_string` | int | `863` | ad_requests_gdpr_applied_valid_consent_string | The number of incoming ad requests for which GDPR is applied, and the consent string is non-null and valid. |
| `ad_requests_GDPR_applied_valid_consent_string_valid_cmp` | int | `564` | ad_requests_GDPR_applied_valid_consent_string_valid_cmp | The number of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is registered with the IAB, as seen [here](https://iabeurope.eu/cmp-list/) |
| `ad_requests_gdpr_applied_valid_consent_string_invalid_cmp` | int | `787` | ad_requests_gdpr_applied_valid_consent_string_invalid_cmp | The number of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is not registered with the IAB, as seen [here](https://iabeurope.eu/cmp-list/) |
| `ad_requests_gdpr_applied_valid_consent_string_tcf_version_1` | int | `986` | ad_requests_gdpr_applied_valid_consent_string_tcf_version_1 | The number of incoming ad requests for which GDPR is applied, the consent string is valid and encoded according to TCF v1. |
| `ad_requests_gdpr_applied_valid_consent_string_tcf_version_2` | int | `600` | ad_requests_gdpr_applied_valid_consent_string_tcf_version_2 | The number of incoming ad requests for which GDPR is applied, the consent string is valid and encoded according to TCF v2. |
| `ad_requests_gdpr_applied_valid_consent_string_xandr_consented` | int | `998` | ad_requests_gdpr_applied_valid_consent_string_xandr_consented | The number of incoming ad requests for which GDPR is applied, and Xandr’s vendor bit (#32) is a 1 in the string for TCF v1 encoded strings |
| `pct_ad_requests_gdpr_country_gdpr_applied` | double | `0.87` | pct_ad_requests_gdpr_country_gdpr_applied | The percentage of incoming ad requests from GDPR-implementing countries for which GDPR is applied. |
| `pct_ad_requests_gdpr_applied_malformed_consent_string` | double | `0.77` | pct_ad_requests_gdpr_applied_malformed_consent_string | The percentage of incoming ad requests for which GDPR is applied, and the consent string is non-blank but malformed. |
| `pct_ad_requests_gdpr_applied_blank_consent_string` | double | `0.83` | pct_ad_requests_gdpr_applied_blank_consent_string | The percentage of incoming ad requests for which GDPR is applied, and the consent string is blank. |
| `pct_ad_requests_gdpr_applied_valid_consent_string` | double | `0.91` | pct_ad_requests_gdpr_applied_valid_consent_string | The percentage of incoming ad requests for which GDPR is applied, and the consent string is non-null and valid. |
| `pct_ad_requests_gdpr_applied_valid_consent_string_valid_cmp` | double | `0.77` | pct_ad_requests_gdpr_applied_valid_consent_string_valid_cmp | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is registered with the IAB, as seen [here](https://iabeurope.eu/cmp-list/)  |
| `pct_ad_requests_gdpr_applied_valid_consent_string_invalid_cmp` | double | `0.76` | pct_ad_requests_gdpr_applied_valid_consent_string_invalid_cmp | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid, and the CMP used to generate the impression is NOT registered with the IAB, as seen [here][https://iabeurope.eu/cmp-list/]. |
| `pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_1` | double | `0.65` | pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_1 | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid and encoded according to TCF v1. |
| `pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_2` | double | `0.55` | pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_2 | The percentage of incoming ad requests for which GDPR is applied, the consent string is valid and encoded according to TCF v2 |
| `pct_ad_requests_gdpr_applied_valid_consent_string_xandr_consented` | double | `0.73` | pct_ad_requests_gdpr_applied_valid_consent_string_xandr_consented | The percentage of incoming ad requests for which GDPR is applied, and Xandr’s vendor bit (#32) is a 1 in the string for TCF v1 encoded strings. |

## Example

### Create a JSON report request

The JSON file should include the `report_type` of `"cmp_analytics"`, as well as the columns (dimensions and metrics) and `report_interval` that you want to retrieve. You can also filter for specific dimensions, define granularity (`month`, `day`), and specify the `"format"` in which the data should be returned (`csv`, `excel`, or `html`). For a full explanation of fields that can be included in the JSON file, see the [Report Service](./report-service.md).

```
$ cat cmp_analytics

{"report":
    {
        "report_type":"cmp_analytics",
        "columns":[
            "day",
            "seller_member_id",
            "call_type",
            "url",
            "ad_requests_gdpr_country",
            "ad_requests_gdpr_applied_valid_consent_string",
            "ad_requests_gdpr_applied_blank_consent_string",
            "ad_requests_gdpr_applied_valid_consent_string_tcf_version_2",
            "pct_ad_requests_gdpr_country_gdpr_applied",
            "pct_ad_requests_gdpr_applied_valid_consent_string",
            "pct_ad_requests_gdpr_applied_blank_consent_string",
            "pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_2",
        ],
        "report_interval":"last_7_days",
        "format":"csv"
    }
}
```
### `POST` a request to the [Report Service](./report-service.md)

`POST` the JSON request to get back a report ID.

```
$ curl -b cookies -X post -d @cmp_analytics "https://api.appnexus.com/report?seller_member_id=123"

{
   "response":{
      "status":"OK",
      "report_id":"09b6979a6a4c3805bdac8921378d3622"
   }
}
```

### `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`. Then use the **report-download** service to save the report data to a file, as described in the next step.

```
$ curl -b cookies 'https://api.appnexus.com/report?id=09b6979a6a4c3805bdac8921378d3622'

{
   "response":{
      "status":"OK",
      "report":{
         "name":null,
         "created_on":"2016-12-11 19:15:48",
         "json_request": "{\"report\":{\"report_type\":\"cmp_analytics\",
             \"columns\":[\"day\",\"seller_member_id\",
             \"call_type\",\"url\",\"ad_requests_gdpr_country\",\"ad_requests_gdpr_applied_valid_consent_string\",\"ad_requests_gdpr_applied_blank_consent_string\",
             \"ad_requests_gdpr_applied_valid_consent_string_tcf_version_2\",\"pct_ad_requests_gdpr_country_gdpr_applied\",
             \"pct_ad_requests_gdpr_applied_valid_consent_string\",\"pct_ad_requests_gdpr_applied_blank_consent_string\",
             \"pct_ad_requests_gdpr_applied_valid_consent_string_tcf_version_2\"],
             \"report_interval\":\"last_7_days\",\"format\":\"csv\",\"filters\":[{\"seller_member_id\":\"123\"}]}}",
             "url":"report-download?id=b97897a7864dd8f34e7457226c7af592"
      },
      "execution_status":"ready"
   }
}
```

### `GET` the report data from the report download service

To download the report data to a file, make another `GET` call with the report ID, but this time to the **report-download** service. You can find the service and report ID in the `url` field of the response to your previous `GET` call. When identifying the file that you want to save to, be sure to use the file extension of the file format that you specified in your initial `POST`.

> [!TIP]
> If an error occurs during download, the response header will include an HTTP error code and message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -b cookies 'https://api.appnexus.com/report-download?id=b97897a7864dd8f34e7457226c7af592' > /tmp/cmp_analytics.csv
```

> [!NOTE]
> There is a limit of 100,000 rows per report when you download them as XLSX and Excel file.
