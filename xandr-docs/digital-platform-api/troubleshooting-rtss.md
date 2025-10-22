---
title: Troubleshooting RTSS
description: In this article, explore ways to troubleshoot Real-Time Signals Service (RTSS).
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Troubleshooting Real-Time Signals Service (RTSS)

This section describes key considerations for managing bulk uploads and campaign targeting.

- [Troubleshooting Real-Time Signals Service (RTSS)](#troubleshooting-real-time-signals-service-rtss)
  - [Bulk upload status](#bulk-upload-status)
  - [Campaigns buying against deactivated targets](#campaigns-buying-against-deactivated-targets)

## Bulk upload status

If you're unsure whether your bulk upload succeeded, you can query the upload ID returned when the bulk upload job was created.

For example, to check the status for upload ID `a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2` uploaded by member 123, run the following cURL command:

```
curl -b cookies https://api.appnexus.com/apd-api/members/123/uploads/a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2 
```

You can also check review the errors file that contains job error information for a completed upload ID.  

For example, below will return a gzipped errors file for upload ID a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2 uploaded by member 123.  Note: job errors files will only be retained for 7 days after processing. 

```
curl -b cookies https://api.appnexus.com/apd-api/members/123/uploads/a04d88c3-8cc7-11e6-868d-7cd30ab7f6e2/errors 
```

The gzip errors file is a csv file with the following fields: 
| Field | Description |
|:---|:---|
| `member_id` | The member ID of the member who submitted the job. |
| `job_id` | The job ID of the job. |
| `submitted_at` | The submission time at which the member submitted the job. |
| `error` | An error string describing the error that was encountered. |
| `line_number` | The line number of the line in the original uploaded file at which the error was encountered. |

The csv file has one row for each error that was encountered during the processing of the customer job (up to 10 rows). 

<!--
The following table shows the possible status returned for the upload overall.

| Status | Description |
|:---|:---|
| `SUBMITTED_1` | The file has been submitted and queued for processing. |
| `PROCESSING_2` | The file is being processed. |
| `COMPLETED_WITH_ERRORS_4` | The file was processed, and most targets have been uploaded properly. However, some lines generated errors, such as negative TTL or a segment access problem, that may have led to problems uploading specific targets. To investigate, check the `message` field in the API response. |
| `COMPLETED_3` | The file was successfully processed, and the resulting targets have been uploaded to the RTSS segments without significant errors. |
| `FAILED_5` | The uploaded file had a significant number of serious errors, and your targets couldn't be uploaded. To investigate, check the `message` field in the API response. After you've fixed the error, try re-uploading the file. |
-->


## Campaigns buying against deactivated targets

Targets that have been uploaded to RTSS with `seg_ttl` values in the future could take a few hours to expire from the RTSS cache after an update is sent to the system. In this case, your segments may continue being added to impressions after you have updated your targeting parameters. This will continue until those targets have expired.
