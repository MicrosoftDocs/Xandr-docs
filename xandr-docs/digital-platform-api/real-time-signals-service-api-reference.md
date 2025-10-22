---
title: Real-Time Signals Service API Reference
description: Explore the Real-Time Signals Service (RTSS) for uploading ID-to-segment data or other key-value data, facilitating the addition of segments to bid requests.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Real-time Signals Service API reference

The RTSS is used to upload ID-to-segment data or other key:value data used to add segments on bid requests.

## API usage

### Regional endpoint URLs

The `regional` endpoint URLs for all RTSS methods is listed below:

| Region | API Endpoint | Detailed reference |
|:---|:---|:---|
| Global | `https://api.appnexus.com/apd-api/` | The default endpoint resolves based on the uploader's origin and directs to either AMER, EMEA or APAC. |
| Americas and EMEA | `https://api.appnexus.com/apd-api-americas/` <br> or `https://api.appnexus.com/apd-api-emea/` | Data published to AMER is automatically replicated to EMEA. Uploads to these datacenters are shared, eliminating the need to upload the same file twice for both regions. |
| APAC | `https://api.appnexus.com/apd-api-apac/` | APAC datacenters operate independently and are not connected to AMER or EMEA.|

### Authentication

Authentication is performed through the [Digital Platform API authentication service](authentication-service.md). The Auth token retrieved from this service must be passed back to the RTSS service via the `Authorization` header, as outlined on the Auth Service page.

### HTTP headers

The following HTTP headers must be appended to your `regional` endpoint calls:

| Method | Required HTTP Headers |
|:---|:---|
| `GET` | `Accept: application/appnexus.apd.vauxhall.v1.0+json`|

## Segment fields

The following segment fields are common to the services listed on this page, and described in the section below:

| Field | Type | Description |
|:---|:---|:---|
| `seg_id` | int | The ID of the segment object. |
| `seg_val` | int | The value associated with the segment for the specified targeting. Segment values have a number of uses, from targetable features in campaigns and [Custom Models](../data-science-toolkit/custom-models.md) to computation inputs for [Bonsai Smart Leaves](../data-science-toolkit/bonsai-smart-leaves.md). The default value for targets uploaded without a `seg_val` is `0`.<br><br>**Note:** When you specify a `seg_val`, use the format `seg_id:seg_val:ttl`. Failure to do so may result in an incorrectly set value. |
| `seg_ttl` | int | The "time to live" for the segment association with the specified targeting. After the TTL duration has passed from the time of upload, the segment will no longer be associated with the specified targeting. Knowing when targets will expire can help you avoid uploading unnecessarily large files. If you need to frequently refresh segments or create new ones, for example when using OLC movement data derived from mobile app, you can also use `seg_ttl` to specify an expiration time period and ensure "old" items are deleted after a specific duration.<br><br>- The default TTL for segments uploaded without a `seg_ttl` value or an `expiry` value is `30` days.<br>- The maximum supported `seg_ttl` value is `365` days.<br><br>**Note:**<br>**`seg_ttl` versus expiry**<br>The TTL you set does not account for any processing delays. In other words, your effective TTL is calculated as TTL minus processing delay. For example, if the file is submitted on `3/1/2022 00:00:00` and processing starts the day after, then the effective TTL is `29` days and the segment expires on `3/31 00:00:00`. If you need to set segment expiration with very specific granularity, you should set it using `expiry`. `expiry` is set for the entire uploaded file, not at the segment level.<br>For the bulk upload format, a `seg_ttl` must be specified as an integer in seconds. For example, `1` day is represented as `86400`.<br><br>For individual uploads, use the following syntax to specify segment TTL durations:<br>- `"ns", "nano"`<br>- `"us", "µs", "micro"`<br>- `"ms", "milli"`<br>- `"s", "sec"`<br>- `"m", "min"`<br>- `"h", "hr", "hour"`<br>- `"d", "day"`<br>- `"w", "wk", "week"`<br><br>**Note:** Where the segment has a known `expiry` value (inherited from the file-level `expiry` setting) as well as a `seg_ttl` value, RTSS uses whichever value results in a shorter TTL. In other words, if the explicit TTL value would result in an earlier expiration, `seg_ttl` will determine the effective TTL. Otherwise, the `expiry` value will take priority.<br>For more information about using this parameter, see "Target Expiry" in [RTSS Best Practices](rtss-best-practices.md). |

## Geo targeting

### REST API ([Open Location Code](https://openlocationcode.com/) - OLC)

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{:member_id}/olcs/{:olc}` | Find segment/value pairs associated with an individual OLC code. |

### Parameters (OLC)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL path | `GET` | `123` |
| `olc` | string | OLC code | URL path | `GET` | `58GR22WM+PW` |

### Response fields (OLC)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `segments` | Array of objects | An array of segments (id: value pairs) | `GET` | See [example](#segments-example). |

#### `segments` example

```
{
"segments": [
{
"seg_id": 555,
"seg_ttl": "1w",
"seg_val": 5050
}
]
}
```

## REST API (postal codes)

> [!NOTE]
> This RTSS functionality is no longer actively supported and is slated to be **deprecated**. You may be able to get the same results from other Xandr products. For assistance, contact your account manager.

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{:member_id}/postal-codes/{:pcode}` | Find segment/value pairs associated with an individual postal code. |

### Parameters (postal codes)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL path | `GET` | `123` |
| `pcode` | string | Postal Code | URL path | `GET` | `07302` |

### Response (postal codes)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `segments` | Array of objects | An array of segments (id: value pairs) | `GET` | See [example](#segments-response-example-postal-codes).  |

#### `segments` response example (postal codes)

```
{
"segments": [
{
"seg_id": 555,
"seg_ttl": "1w",
"seg_val": 5050
},
{
"seg_id": 626,
"seg_ttl": "2d3h",
"seg_val": 0
}
]
}
```

## REST API (IP address)

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{:member_id}/ips/{:ip}` | Find segment/value pairs associated with an individual IP. |

### Parameters (IP address)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL Path | `GET` | `123` |
| `ip` | string | An individual IP address. | URL Path | `GET` | `192.168.0.20` |

### Response (IP address)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `segments` | Array of objects | An array of segments (id: value pairs). | `GET` | See [example](#segments-response-example-ip-address). |

#### `segments` response example (IP address)

```
{
"segments": [
{
"seg_id": 555,
"seg_ttl": "1w",
"seg_val": 5050
},
{
"seg_id": 626,
"seg_ttl": "1m2d30m",
"seg_val": 0
}
]
}
```

## URL targeting

### REST API (URL components)

Target URL components with `"OR"` logic, with up to 3 paths.

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{:member_id}/urls/components` | Find segment/value pairs targetable by URL Components. |

### Parameters (URL components)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL Path | `GET` | `123` |
| `path` | string | Partial URL | Query string | `GET` |  `mysampledomain.com/en/buyers` |

#### `path` example

```
mysampledomain.
mysampledomain.com
mysampledomain.com/en
mysampledomain.com/en/buyers
mysampledomain.com/en/buyers/mysampledomain-test
/en
/en/buyers
/en/buyers/mysampledomain-test
```

#### `segval_list` example

```
[
{
"seg_id": 123,
"seg_ttl": "30m",
"seg_val": 345
}
]
```

### Response (URL components)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `segments` | Array of objects | An array of segments (id: value pairs) | `GET` | See [example](#segments-response-example-url-components). |

#### `segments` response example (URL components)

```
{
"segments": [
{
"seg_id": 555,
"seg_ttl": "1w",
"seg_val": 5050
},
{
"seg_id": 626,
"seg_ttl": "2d20m",
"seg_val": 0
}
]
}
```

## REST API (URL reference)

Target Full URL with exact matching.

| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{:member_id}/urls/reference` | Find segment/value pairs targetable by URL. |

### Parameters (URL reference)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL Path | `GET` | `123` |
| `path` | string | Full URL<br>URL should contain only secondary and top-level domains of the host section of the authority URL part, and full path that will be matched exactly. | Query Parameter | `GET` | `mysampledomain.com/as/many/paths/as/i/want`<br>URLs will be matched exactly as they have been uploaded. |

### Response (URL reference)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `segments` | Array of objects | An array of segments (id: value pairs) | `GET` | See [example](#segments-response-example-url-reference). |

#### `segments` response example (URL reference)

```
{
"segments": [
{
"seg_id": 555,
"seg_ttl": "1w",
"seg_val": 5050
},
{
"seg_id": 626,
"seg_ttl": "2d20m",
"seg_val": 0
}
]
}
```

> [!NOTE]
> Uploaded IDs are converted to lower-case values when stored. Matching is not case-sensitive.

## Uploads

### REST API (Bulk upload)

The maximum size for a single upload may not exceed 256 MB. Ensure that you compress your files using GZIP before uploading to RTSS.

| Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `/members/{:member_id}/uploads` | Bulk upload endpoint. |
| `GET` | `/members/{:member_id}/uploads/{upload_job_id}` | Get job status of a single upload job. |


### Parameters (Bulk upload)

| Name | Data Type | Description | Parameter Type | Required On | Example |
|:---|:---|:---|:---|:---|:---|
| `member_id` | long | Member ID | URL Path | All Methods | `123` |
| `id` | string | UUID of Accepted File Job | Query string |  | `102951` |
| `Upload_job_id` | string | UUID of Accepted File Job  | URL path | GET | a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2 |
| `Content-Type` | string | The Content-Type HTTP Header | HTTP Header | `POST` | `'Content-Type: multipart/form-data'` |
| `file` | file | The data file to be processed. Max file size of 256 MB | Form Data | `POST` | See [File Format and Examples](#file-format-and-upload-examples) section below. |
| `expiry` | date | The fixed time and date when the segments in the file should expire, taking into account any processing time required to meet the deadline. For more information about using this parameter, see "Target Expiry" in [RTSS Best Practices](rtss-best-practices.md). | [RFC 339](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) | POST (Optional) | `expiry=2022-03-01T17:32:28Z` |

### Response (Bulk upload)

| Name | Data Type | Description | Returned On | Example |
|:---|:---|:---|:---|:---|
| `uploads` | Object | Object containing upload info for the specified job id  | `GET` | See [example](#uploads-response-example-bulk-upload). |
| `id` | string | uuid of accepted file which will be processed asynchronously | `POST` | See [example](#id-response-example-bulk-upload). |

#### `uploads` response example (Bulk upload)

```
{ 
  "added": "string", 
  "id": "string", 
  "member_id": 0, 
  "records_failed": 0, 
  "records_total": 0, 
  "status": "string", 
  "stopped": "string" 
} 
```

#### `id` response example (Bulk upload)

```
{
"id": "a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2"
}
```

### REST API (job errors) 

This method provides a gzipped errors file containing job error details for a completed upload job, if errors occurred in the submitted data. 

> [!NOTE] 
> Error files are retained for 7 days after processing. 
| Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `/members/{member_id}/uploads/{upload_job_id}/errors` | Get job errors file for a single upload job. |

#### Parameters (job errors) 

| Name | Parameter type | Data type | Required? | Description | Example usage |
|:---|:---|:---|:---|:---|:---|
| `member_id` | path | long | yes | ID of the member | /members/1/uploads/66f0cc9e-161b-11f0-b84c-00163e21c952/errors |
| `upload_job_id` | path | string (uuid) | yes | UUID of Accepted Uploaded File Job | /members/1/uploads/66f0cc9e-161b-11f0-b84c-00163e21c952/errors |

#### Response (job errors) 

Successful response (200) returns gzip file (Response content type: application/gzip) containing detailed information about job errors. 

Alternative possible response codes: 
-  403
- 404
- 500 

The gzip errors file is a csv file with the following fields: 

| Field | Description |
|:---|:---|
| `member_id` | The member ID of the member who submitted the job. |
| `job_id` | The job ID of the job. |
| `submitted_at` | The submission time at which the member submitted the job. |
| `error` | An error string describing the error that was encountered. |
| `line_number` | The line number of the line in the original uploaded file at which the error was encountered. |

The csv file has one row for each error that was encountered during the processing of the customer job (up to 10 rows). 



### HTTP status codes (Bulk upload)

| Status Code | Returned On | Reason | Headers | Header Description |
|:---|:---|:---|:---|:---|
| `200` | `GET`, `POST` | Success | `X-AuditID` | Reference Audit ID |

### File format and upload examples

#### File format

| **`keytype`** | separator | **`key`** | separator | **`action`** | separator | **`segment`** | separator | **`segment`** |

- **Columns**: `keytype`, `key`, `action`, `segment`
- **Separators**: comma `,` or tab `0x09` `\t` (csv or tsv files)
- **Line separator**: `0x0A` `\n`
- Representation of each column must be less or equal to **`32,767` byt `keytype` and `key` Columns**

| `keytype` ID | Type | `key` Examples |
|:---|:---|:---|
| `0` | string | - Single IP address: `"127.0.0.1"` |
| `2` | string | Geo hashcode in OLC format:<br>[OLC spec](https://openlocationcode.com/) |
| `3` | string | Postal code<br>**Note:** Postal codes targets will be **deprecated** soon.<br>`"11235"` |
| `4` | string | Partial URL (up to 3 paths)<br>- `mysampledomain.com`<br>- `mysampledomain.com/en/buyers`<br>- `mysampledomain.com/en/buyers/page` |
| `6` | string | Full URL<br>`mysampledomain.com/many/paths/are/supported` |

##### `action` column

| ID | Description |
|:---|:---|
| `0` | Add to segment |
| `1` | Remove from segment |

##### `segment` column

The segment column can contain:

- `segment_id;segment_id`
- `segment_id:segment_value`
- `segment_id:segment_value:segment_ttl`

When only the `segment_id` is provided, RTSS will assume that segment value is `0`, and segment a TTL of `default` (30 days).

`segment_ttl` must be an integer, indicating TTL duration in **seconds** only.

###### Example CSV file

The header row in the sample file below can be excluded. The bulk upload service will accept files with or without a header.

```
keytype,key,action,segment
0,"63.148.81.22,63.148.81.22",0,1000
1,"US,US:KY",0,1001
1,"US,US:NJ",0,1001:22
2,"8FGQGG00+",0,1002
4,"mysampledomain.",0,1008:10
4,"/en/buyers",0,1004;1005;1006
4,"mysampledomain.com/en",0,1008:25:86400
5,123e4567-e89b-12d3-a456-426655440000,0,1005
6,"mysampledomain.com/many/paths/exact/match",0,1009
```

#### Example `POST` method

##### `POST` request using cURL

```
curl -X POST --header 'Content-Type: multipart/form-data' \
-F file=@"member-1-test.csv.gz"  'https://api.appnexus.com/apd-api/members/1/uploads'
```
or

```
curl -X POST --header 'Content-Type: multipart/form-data' \ -F file=@"member-1-test.csv.gz"  'https://api.appnexus.com/apd-api-emea/members/1/uploads'
```


##### JSON response

Server responds with the job ID.

```
{ "id": "a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2" }
```

#### Example `GET` method

##### `GET` request using cURL

```
curl https://api.appnexus.com/apd-api/members/1/uploads/a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2 
```

##### `GET`: JSON response

Server responds with information about the job ID specified in the Query Parameters.

```
{
    "uploads": [
        { 

          "added": "2016-10-07T19:52:49Z", 
          "id": " a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2", 
          "member_id": 1, 
          "records_failed": 2, 
          "records_total": 3, 
          "status": " completed_with_errors", 
          "stopped": "2016-10-07T19:52:49Z" 

        } 
    ]
}
```
<!--
> [!NOTE]
>
> - The `rows_failed` field indicates how many lines failed to process.
> - The `message` field is an error description for failed lines. It returns a maximum of 100 errors.
-->


## Best upload practices

For more information about Bulk Uploads, see [RTSS Best Practices](./rtss-best-practices.md).
