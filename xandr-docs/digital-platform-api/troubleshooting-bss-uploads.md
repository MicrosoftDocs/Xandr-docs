---
title: Digital Platform API - Troubleshooting BSS Uploads
description: Use the methods povided in this article to diagnose any problems with your segment data upload and troubleshoot them.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Troubleshooting BSS uploads

You can use the methods in this topic to diagnose any problems with your segment data upload.

## Different phases of batch segment service

This section describes the phases of upload, so you can understand where problems may be occurring.

### Starting - Request upload URL and Job ID

In this phase, the clients request an upload URL and a job ID. This stage times out in 5 minutes. If jobs are stuck in this phase, it indicates that the clients requested the URL but failed to upload anything within the allotted time.

### Uploading

In this phase, the clients upload the file to the given URL. It is recommended not to exceed one upload per minute. If the clients have more than 200 jobs waiting to be processed at any given time, they will be prohibited from uploading additional jobs.

### Validating and processing

Once the clients upload the file, processing of the file occurs in the next phase where the validation of segment IDs and user IDs is carried out. If a record contains invalid segment or user IDs, the platform does not process the record. When the clients check the job status, they will be able to view statistics regarding the number of invalid users.

### Completion

In this phase, the data of the file is successfully uploaded to the platform, and it is available for targeting.

## Possible upload errors

### Attempting to upload file larger than 0.5GB

```
{"response":{"status":"ERROR","error_code":"FILESIZE_LIMIT_EXCEEDED","errors":["Member exceeds maximum byte size allowed for a file"]}}
```

### Error code in batch segment upload job

```
""batch_segment_upload_job": {
      "phase": "error",
      "start_time": "2015-08-13 18:40:32",
      "uploaded_time": null,
      "validated_time": null,
      "completed_time": null,
      "error_code": "uploading-error",
      "time_to_process": "0.00",
      "percent_complete": 0,
      "num_valid": 0,
      "num_invalid_format": 0,
      "num_valid_user": 0,
      "num_invalid_user": 0,
      "num_invalid_segment": 0,
      "num_invalid_timestamp": 0,
      "num_unauth_segment": 0,
      "num_past_expiration": 0,
      "num_inactive_segment": 0,
      "num_other_error": 0,
      "error_log_lines": null,
      "segment_log_lines": null,
      "id": 11661553,
      "job_id": "Pm3oCUf5CSVKIOt4mAqOzdt6K3qInj1431542432",
      "member_id": 958,
      "created_on": "2015-05-13 18:40:32",
      "last_modified": "2015-05-13 18:40:33"
    }
```

**The following errors may happen when**:

1. You have reached one of its four upload limits:

    - daily bytes,
    - hourly bytes,
    - daily lines, or
    - hourly lines

    Attempting to exceed daily byte upload limit

    ```
    {"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
                      exceeds maximum allowed bytes per day"]}}
    ```

    Attempting to exceed hourly byte upload limit

    ```
    {"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
                      exceeds maximum allowed bytes per hour"]}}
    ```

    Attempting to exceed daily lines upload limit

    ```
    {"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
                      exceeds maximum allowed number of lines per day"]}} 
    ```

    Attempting to exceed hourly lines upload limit

    ```
    {"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
                      exceeds maximum allowed number of lines per hour"]}}
    ```

1. You have canceled the upload.
1. The upload phase exceeds 90 minutes.
    Exceeding maximum time to upload

    ```
    {"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Maximum
                      upload time exceeded"]}}
    ```

## Possible processing errors

### Invalid format

If the value of the `num_invalid_format` field is greater than `"0"`, check the values in the `error_log_lines` field.

In the example below, the `num_invalid_format` field displays a value of `"1"`, with details provided in the `error_log_lines` field.

In the `error_log_lines` field:

- `num_invalid_format` indicates that there was a problem parsing a line in the uploaded file.
- `"failed with an illegal number of fields"` indicates that the number of fields in a `segment_fields` block did not match what was defined in the batch-segment config (for more information, see [Initial BSS Account Setup](./initial-bss-account-setup.md)).

In this case, the config expects three fields to be defined in the block: `SEG_ID`, `VALUE`, `EXPIRATION`, but the parser only found two fields - `SEG_ID` and `VALUE`, thus showing an error.

### `num_invalid_format` and `error_log_lines` example

```
"batch_segment_upload_job": {
phase": "completed",
"error_code": null,
"time_to_process": "0.01",
"percent_complete": 100,
"num_valid": 0,
"num_invalid_format": 1,
"num_valid_user": 0,
"num_invalid_user": 0,
"num_invalid_segment": 0,
"num_invalid_timestamp": 0,
"num_unauth_segment": 0,
"num_past_expiration": 0,
"num_inactive_segment": 0,
"num_other_error": 0,
"error_log_lines": "num_invalid_format-WINDOWSADID-USER-ID;SEG_ID:VALUE~9 failed with an illegal number of fields",
"segment_log_lines": null,
"start_time": "2015-08-13 18:40:32",
"uploaded_time": "2015-08-13 18:42:32",
"validated_time": "2015-08-13 18:42:32",
"completed_time": "2015-08-13 18:42:33",
"id": 123412341234,
"job_id": "Pm3oCUf5CSVKIOt4mAqOzdt6K3qInj1431542432",
"member_id": 958,
"created_on": "2015-08-13 18:40:32",
"last_modified": "2015-08-13 18:42:33"
}
```

## View your file upload history

To see metadata about all your segment file uploads within the last 30 days, make a `GET` call to the service with your `member_id` specified in the query string. The JSON response will include an array of `batch_segment_upload_job` objects.

For more information about the specific fields of the `batch_segment_upload_job` object, see [JSON fields](#json-fields).

> [!NOTE]
> File upload history is available for the last 30 days only.

```
$ curl -b cookies 'https://api.appnexus.com/batch-segment?member_id=456'

{
   "response" : {
      "batch_segment_upload_job" : [
         {
           "phase": "completed",
            "start_time": "2012-05-22 16:48:55",
            "uploaded_time": "2012-05-22 16:48:56",
            "validated_time": "2012-05-22 16:49:01",
            "completed_time": "2012-05-22 16:49:01",
            "error_code": null,
            "time_to_process": "0.04",
            "percent_complete": 100,
            "num_valid": 0,
            "num_invalid_format": 0,
            "num_invalid_user": 2,
            "num_invalid_segment": 0,
            "num_unauth_segment": 1,
            "num_past_expiration": 0,
            "num_inactive_segment": 0,
            "num_other_error": 0,
            "error_log_lines": " \n\nnum_unauth_segment-4013681496264948522;5013:0,5014:1550\nnum_invalid_user-7652266028043224430;5848:0,5849:1440,5850:1440\nnum_invalid_user-8802117132500293405;5851:0,5847:-1",
            "id": 98,
            "job_id": "T1v98eIOlCZndeLGSXD0nrs57L8ES11337705335",
            "member_id": 456,
            "created_on": "2012-05-22 16:48:55",
            "last_modified": "2012-05-22 16:49:01"
         },
     ...
    }
  }
}
```

> [!NOTE]
> Our API limits responses to 100 objects via pagination. You can view additional objects by appending one of these to the API call:
>
> - `&start_element=101`
> - `&sort=last_modified.desc`
>
> You can read more about pagination on our Documentation Portal [here](./05---throttling-pagination-and-filtering.md).
>
> If you're still experiencing technical issues, you can submit a request on our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com). Don't forget to include the job ID in your support request.

## JSON fields

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/batch-segment/meta` | Use this call to find out which fields you can filter and sort by. |

| Fields | Type | Description |
|:---|:---|:---|
| `id` | int | This is the ID of the `batch_segment_upload_job` object associated with this request.<br><br>**Default**: An automatically generated number. |
| `status` | string | The status of the API call; successful calls return `"OK"`. |
| `batch_segment_upload_job` | object | This is an object whose fields contain metadata describing the upload and processing job. If you are using the Impbus API, this will be an array containing a single object. See [Batch Segment Upload Job](#batch-segment-upload-job) for details. |

### Batch segment upload job

When you request the status of your processing job, the system returns a `batch_segment_upload_job` object (if you are a data provider, this will be an array containing a single object). Depending on which request you're making to the service, it will contain some or all of the following metadata.

> [!NOTE]
> Most metadata will only be present when `"phase": "completed"`.

| Fields | Type | Description |
|:---|:---|:---|
| `upload_url` | string | The URL where you'll upload your segment data file. |
| `phase` | enum | The current processing status.<br><br>Returns one of the following values:<br> - `error`<br> - `starting`<br> - `uploading`<br> - `validating`<br> - `processing`<br> - `completed` |
| `start_time` | date | The time at which file upload began. |
| `uploaded_time` | date | The time at which the file associated with this job ID was uploaded. |
| `validated_time` | date | The time at which file validation was completed. |
| `completed_time` | date | The time at which file processing was completed. |
| `error_code` | int | If `"phase": "error"`, this error code describes the type of error encountered. Note that an error code will only be shown here if there was an error with the uploading, validating, or processing of the file itself (i.e., does not include invalid format or invalid segment errors). Common errors are caused by unreadable files and exceeding defined object limits.<br><br>Returns `null` if no errors were found. |
| `time_to_process` | decimal | The time it took to process the segment file, in minutes. |
| `percent_complete` | int | The percentage of the processing that has been completed, given the current phase at the time of the request. |
| `num_valid` | int | The number of valid lines in the uploaded file. Each user/segment combination is considered 1 line. |
| `num_invalid_format` | int | The number of uploaded lines containing formatting errors. This depends upon your particular file format configuration. Duplicate lines will also be considered an invalid format. |
| `num_valid_user` | int | A count of unique input lines that have a valid user ID. |
| `num_invalid_user` | int | A count of unique input lines that have an invalid or non-existent user. |
| `num_invalid_segment` | int | The number of invalid segments in the file. Deduplicated. |
| `num_invalid_timestamp` | int | The number of invalid timestamps in the file. |
| `num_unauth_segment` | int | The number of segments in the file which you are unauthorized to access. Deduplicated. |
| `num_past_expiration` | int | The number of expired segments in the file. Deduplicated. |
| `num_inactive_segment` | int | The number of inactive segments in the file. Deduplicated. |
| `num_other_error` | int | This is a placeholder value not currently in use. |
| `error_log_lines` | string | A string containing newline-separated lines. Each line lists a validation error or the reason for an error while uploading your file.<br><br>You can choose how many lines appear in this field.<br><br>**Default**: `200 lines` |
| `segment_log_lines` | string | A string containing newline-separated lines consisting of the segment ID and the number of users successfully added or removed. This field defaults to `200 lines`.<br>The format is added: `SEG_ID:COUNT SEG_ID:COUNT ... removed: SEG_ID:COUNT ...` where `SEG_ID` is the segment ID and `COUNT` is the number of users successfully added or removed. `SEG_ID:COUNT` pairs are sorted by `COUNT` (descending).<br><br>Example:<br>`added:15889133:38622115547290:186227removed:15889278:36973415889206:25530715889179:232831` |
| `id` | int | The unique identifier of this object. |
| `job_id` | string | A string of alphanumeric characters that uniquely identifies the processing job associated with this file. |
| `member_id` | int | Your member ID.<br><br>**Required On**: `PUT`, `POST` |
| `created_on` | date | The creation date of this object. |
| `last_modified` | date | The most recent modification date of this object (usually via `POST`). |

## Related topics

- [Legacy BSS File Format](./legacy-bss-file-format.md)
- [Batch Segment Service Best Practices](./batch-segment-service-best-practices.md)
