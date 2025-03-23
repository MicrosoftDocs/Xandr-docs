---
title: Real-Time Signals Service (Formerly APD)
description: Explore the Real-Time Signals Service (RTSS) that enables segment creation and targeting based on real-time signals.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# RTSS Overview

## Introduction

RTSS is not generally available to all clients. Contact your account manager for access.

RTSS enables audience targeting using the following real-time signals:

- **IP address**
- **URL path**
- **Geo-targeting**
- **Open location codes (OLC) (8-character codes)**

It is a scalable alternative to cookie-based audience targeting.

### GDPR and the phase-out of third-party cookies

With evolving privacy regulations and increased scrutiny on user data collection—along with ad-blocking—reliance on cookies and other device IDs is becoming increasingly difficult.

### CTV and the cookie-less environment

There is no universal or persistent standard for device identification in CTV. The CTV ecosystem is dominated by a few "walled gardens." As a result, advertisers and agencies must either collaborate directly with each device maker/platform or buy through Private Marketplace (PMP) deals.

## Limitations

- **Reporting constraints:** Reporting on uploaded targets is available only by segment.
- **Exclusion targeting limitations:** RTSS segments do not support exclusion targeting.
- **TTL restriction:** The maximum time-to-live (TTL) for a targeting feature is 365 days.
- **Regionalized storage:** Uploads have regionalized API endpoints and storage locations.

## Use cases

### Publishers

For publishers and their data management platforms (DMPs), RTSS provides a secure, privacy-compliant alternative for onboarding and monetizing first-party (1P) audiences using contextual signals.

### Curators

Curators can use RTSS to create context-based audiences using alternative signals. They can then pair this audience data with supply from the Xandr exchange to create media products, which can be sold through deals to any demand-side platform (DSP).

### Buyers

Buyers can use RTSS to create their own audiences or access premium publishers' audiences. This enables targeting in cookie-less environments, such as connected TV (CTV).

## Best practices

### Targeting features

- **Reduce shared targeting features:** Consolidate shared targeting features across multiple segments to simplify management.
- **Use feature targeting for reporting:** Instead of querying by segment, use feature targeting to improve organization and TTL management.
- **Manage TTL effectively:**
  - Use shorter TTLs (30 days) for better management.
  - Monitor TTL/expiry times to prevent targeting decay.
  - Replenish targeting features predictably (e.g., refresh every 30 days when using a 30-day TTL).
  - Use the expiry feature on file upload for precise expiration control.
- **Upload only deltas:** Uploading only the differences helps reduce processing time.
- **Optimize OLC targeting:** Use 8-character OLC symbols (~275m block) for optimal results.

### File format requirements

- **Compression:** Compress CSV bulk uploads using GZIP.
- **File format:**
  - Save files in UTF-8 without BOM encoding.
  - Use Unix-style line endings (line feed, not carriage return).
  - Ensure files do not contain a trailing line ending.

### Upload process

- **API rate limiting:** Use 3-5 second retries to prevent throttling.
- **Regionalized storage:** Data uploaded to a specific region is not interoperable. If using RTSS across multiple regions, upload data to the appropriate regional endpoints.

### Campaign considerations

- **Exclusion targeting is not supported:** RTSS segments cannot be excluded when applied to line items.

## Regional Support

RTSS data is not interoperable across regions. To use RTSS across multiple regions, upload data to the desired regions.

If unsure, reach out to your account manager.

### Endpoints

| Region    | Endpoint                                           | Notes |
|-----------|---------------------------------------------------|-------|
| Global    | `https://api.appnexus.com/apd-api/`              | Default endpoint resolves to either AMER/EMEA or APAC based on uploader origin. |
| Americas  | `https://api.appnexus.com/apd-api-americas/`     | Data published to AMER is replicated to EMEA. |
| EMEA      | `https://api.appnexus.com/apd-api-emea/`         | Uploads to these datacenters are shared and do not require duplicate uploads. |
| APAC      | `https://api.appnexus.com/apd-api-apac/`         | APAC datacenters are isolated from AMER/EMEA. |

### Select the right endpoint

- If unsure how to regionalize data but do not need APAC, use the **Default** endpoint.
- If unsure how to regionalize data but need it globally, including APAC, send data to **both Default and APAC endpoints**.
- If data is regionalized, send it exclusively to the appropriate regional endpoint.

## RTSS workflow

The following steps are required for utilizing RTSS:

| Step                              | Endpoint                                    | Notes |
|-----------------------------------|---------------------------------------------|-------|
| Authenticate via [Auth API](authentication-service.md)         | `POST https://api.appnexus.com/auth`       |       |
| Create a segment via [Segment API](segment-service.md)  | `POST https://api.appnexus.com/segment`    | Segments must be created before uploading RTSS targets. |
| Upload CSV file via REST API      | `POST /members/{member_id}/uploads`       | Max file size: 256MB (recommended compression: GZIP). |
| Check upload status               | `GET /members/{member_id}/uploads`        | Uploads take up to 24 hours to process. |
| Validate targeting features       | `GET /members/{member_id}/olcs/{olc}`     | Reports are accessible by querying uploaded targeting features. |

## Bulk Upload file format

### File format requirements

The requirements for formatting the CSV file are:

- **Encoding:** ASCII or UTF-8 without BOM  
- **Columns:** `keytype`, `key`, `action`, `segment(s)`  
- **Separator:** Comma (`','`) or tab (`0x09`, `'\t'`)  
- **Line separator:** `0x0A` (`'\n'`)
- Each column can be no larger than **32,767** bytes  

## Example CSV data for bulk upload

The header row in the sample file below is optional. The bulk upload service accepts files with or without a header. Refer to the API documentation for more details.  

```
keytype,key,action,segment 
0,"63.148.81.22,63.148.81.22",0,1000 
2,"8FGQGG00+",0,1002 
4,"mysampledomain.",0,1008:10 
4,"/en/buyers",0,1004;1005;1006 
4,"mysampledomain.com/en",0,1008:25:86400 
6,"mysampledomain.com/many/paths/exact/match",0,1009 
```

## Upload CSV files

The maximum file size for a single upload is **256 MB**. Ensure that you compress files using **GZIP** before uploading to RTSS.

### API upload

| Method | Endpoint | Description |
|--------|---------|-------------|
| `POST` | `/members/{member_id}/uploads` | Upload a CSV file (can be GZIP compressed). |

#### Example API request

```sh
curl -X POST --header 'Content-Type: multipart/form-data' \
-F file=@"member-1-test.csv.gz" 'https://api.appnexus.com/apd-api-americas/members/1/uploads'
```

#### Successful response

A successful response returns a job ID to check the file processing status.

```json
{ "id": "a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2" }
```

## Monitor upload status

Uploads take up to **24 hours** to process before being available for targeting.

| Method | Endpoint | Description |
|--------|---------|-------------|
| `GET` | `/members/{member_id}/uploads` | Get a list of active uploads. |

#### Example status request

```sh
curl https://api.appnexus.com/apd-api/members/1/uploads?id=a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2
```

#### Example response

```json
{
  "uploads": [
    {
      "added": "2016-10-07T19:52:49Z",
      "id": "a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2",
      "member_id": 1,
      "rows_total": 6,
      "rows_failed": 1,
      "records_total": 8,
      "records_failed": 2,
      "message": "5: bad ip range",
      "started": "2016-10-07T19:52:49Z",
      "status": "completed_with_errors",
      "stopped": "2016-10-07T19:52:49Z"
    }
  ]
}
```

> [!NOTE]
> 
> - The `rows_failed` field indicates how many lines failed to process.
> - The `message` field provides an error description for failed lines (maximum 100 errors).

## Validate targeting features

After successfully uploading targeting features, manage them by looking up assigned segments.

| Method | Endpoint | Description |
|--------|---------|-------------|
| `GET` | `/members/{member_id}/olcs/{olc}` | Find segment/value pairs associated with an individual OLC code. |
| `GET` | `/members/{member_id}/ips/{ip}` | Find segment/value pairs associated with an individual IP. |
| `GET` | `/members/{member_id}/urls/components` | Find segment/value pairs targetable by URL Components. |
| `GET` | `/members/{member_id}/urls/reference` | Find segment/value pairs targetable by URL. |

#### Example request

```sh
curl https://api.appnexus.com/apd-api-emea/members/1/urls/components?path=acme.com/clothing
```

#### Example response

```json
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

## RTSS support

If you encounter issues or need guidance, open a case in the **Xandr support portal**. For feedback on the beta, contact your account management team.

## Bugs and breaking changes

The RTSS beta is updated frequently based on participant feedback. Expect occasional platform issues, and ensure your team is prepared to adapt to changes.

> [!IMPORTANT]
>
> - Standard **Breaking Change** notification policies and timelines do **not** apply to this beta feature.
> - Monitor all communications from Xandr regarding RTSS beta updates.
> - Be prepared to modify implementations as needed.
