---
title: Bidders - Batch Segment Service API
description: In this article, find information about the Batch Segment Service (BSS), how to use the feature, possible errors you might face, and the JSON fields associated with BSS.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - Batch segment service API

The Batch Segment Service allows you to upload audiences to the Xandr platform through a batch/bulk upload framework. This data can be used in conjunction with data from buyers or sellers for the purposes of campaign targeting or yield management. All data sent through the Batch Segment Service is appended to the existing segment data already in our system.

Features include:

- Ability to upload compressed files
- Error checking of segment data
- Configurable input file format
- Confirmation of successful upload
- Feedback on overall processing status
- Association of segments to users regardless of location of users
- A high maximum data volume

For optimal results, it is strongly recommended to implement the best practices found in [Batch Segment Service Best Practices](batch-segment-service-best-practices.md).

> [!NOTE]
> The Batch Segment Service requires configuration prior to use. Please consult [Initial BSS Account Setup](initial-bss-account-setup.md) to learn how to configure it for your seat.
> [!IMPORTANT]
> **Gzip** is the only file compression method supported by this service.

## Add a segment file for processing

Adding your segment file to the system is a three-step process. First, request a job identification number and upload URL. Second, upload your file to the assigned upload URL. Third, check the job's processing status. Please note that for now, files are limited to at most 1800 segments on any individual line. If you have more than 1800 segments for one user you must break that line into multiple lines.

- [Step 1. Request an upload URL and job ID](#step-1-request-an-upload-url-and-job-id)
- [Step 2. Post the file to the upload URL](#step-2-post-the-file-to-the-upload-url)
- [Step 3. Check the job status](#step-3-check-the-job-status)

### Step 1. Request an upload URL and job ID

Each segment data file that is uploaded must be associated with a particular job ID. This ID is used to create the upload URL and to track the file's processing status. The first step is to send an empty `POST` request to the service.

> [!NOTE]
> This service works for both `api.appnexus.com` and for `api.adnxs.com` - it is available for both bidder and console logins.

```
$ curl -b cookies -X POST "https://api.appnexus.com/batch-segment?member_id=456"
{
 "response": {
  "id": 123,
  "status": "OK",
  "batch_segment_upload_job": {
   "job_id": "JFY8l6iMOFAFJIWCMPcy39MCt3Yleo1337618549",
   "id": 123,
   "member_id": 456,
   "last_modified": "2012-05-21 16:42:29",
   "upload_url": "https://01.data-api.prod.adnxs.net/segment-upload/JFY8l6iMOFAFJIWCMPcy39MCt3Yleo1337618549"
  },
  "start_element": 0,
  "count": 1,
  "num_elements": 100,
  "dbg_info": {
  ...
  }
 }
}
```

### Step 2. Post the file to the upload URL

The file upload URL is given in the JSON response to Step 1 by the field `upload_url`. You must `POST` your segment file to this URL for processing. You'll receive a JSON object that tells you if the upload succeeded. Do not hardcode the upload URL in your application - make sure to dynamically grab it from the `upload_url` field.

> [!NOTE]
>
> - You must begin your upload to the given Upload URL within five (5) minutes, and only one URL is valid at any given time. If you wait longer than 5 minutes to start your upload you must request a new URL.
> - We recommend you do not exceed one upload per minute. If you have more than 200 jobs waiting to be processed at any given time, you will be prohibited from uploading additional jobs.
> - Your segment file should not be larger than 0.5GB.
> [!WARNING]
> In order for the file to upload correctly, you *must* specify the MIME type in the HTTP header as "Content-Type: application/octet-stream". *Do not* use "Content-Type: application/x-www-form-urlencode" (-d or --data flags in curl). Using an incorrect MIME type will prevent the file from being processed by the API Batch Segment Service.
>
> Your file must conform to the Latin1 character set.

```
$ curl -v -H 'Content-Type:application/octet-stream' -b cookies -X POST --data-binary @segment_file "https://01.data-api.prod.adnxs.net/segment-upload/JFY8l6iMOFAFJIWCMPcy39MCt3Yleo1337618549"
* About to connect() to 01.data-api.prod.adnxs.net port 80
*   Trying 64.210.62.71... connected
* Connected to 01.data-api.prod.adnxs.net (64.210.62.71) port 80
> POST /segment-upload/FkmOY7oL2Qy2aCE7NrhE1BHVoJA0wi1337697712 HTTP/1.1
> User-Agent: curl/7.15.5 (x86_64-redhat-linux-gnu) libcurl/7.15.5 OpenSSL/0.9.8b zlib/1.2.3 libidn/0.6.5
> Host: 01.data-api.prod.adnxs.net
> Accept: */*
> Content-type:application/octet-stream
> Content-Length: 116
>
> 7652266028043224430;5848:0,5849:1440,5850:14404013681496264948522;5013:0,5014:15508802117132500293405;5851:0,5847:-1HTTP/1.1 200 OK
< Date: Tue, 22 May 2012 14:48:02 GMT
< Content-Type: application/json
< Transfer-Encoding: chunked
< Server: Jetty(7.6.2.v20120308)
* Connection #0 to host 01.data-api.prod.adnxs.net left intact
* Closing connection #0
{"response":{"segment_upload":{"job_id":"FkmOY7oL2Qy2aCE7NrhE1BHVoJA0wi1337697712"},"status":"OK"}}
                     
```

#### Example of SSL upload URL

```
curl -b cookie -c cookie -X POST -s -d '' "https://api.appnexus.com/batch-segment?member_id=958"
"batch_segment_upload_job": {
      "id": 14841671,
      "job_id": "qGQhSZ1qvd2hSsJ9svTz32qgxq7z5b1439315424",
      "member_id": 958,
      "last_modified": "2015-08-11 17:50:24",
      "upload_url": "https://data-api-gslb.adnxs.net/segment-upload/qGQhSZ1qvd2hSsJ9svTz32qgxq7z5b1439315424"
    }
```

### Step 3. Check the job status

Finally, check the processing status by sending a `GET` request. The JSON response contains information such as how long the file took to process and the number of errors, if any. Note that you should wait until `"phase": "completed"` before looking at the results fields such as
`num_valid`. For more detailed information, see [JSON Fields](#json-fields) below.

> [!NOTE]
> Per Xandr SLA, allow up to 24 hours for the file to process.
> [!WARNING]
> If you are a data provider using the Impbus API, note that the `batch_segment_upload_job` field will be an array with a single object inside of it, e.g.:
>
> ```
> {"batch_segment_upload_job":[{"phase": "completed"}]}
> ```
>

```
$ curl -b cookies "https://api.appnexus.com/batch-segment?member_id=456&job_id=JFY8l6iMOFAFJIWCMPcy39MCt3Yleo1337618549"
{
 "response": {
  "start_element": 0,
  "count": 1,
  "batch_segment_upload_job": {
   "phase": "completed",
   "start_time": "2012-05-21 20:04:35",
   "uploaded_time": "2012-05-21 20:04:41",
   "validated_time": "2012-05-21 20:07:24",
   "completed_time": "2012-05-21 20:08:24",
   "error_code": null,
   "time_to_process": "2.69",
   "percent_complete": 100,
   "num_valid": 200000,
   "num_valid_user":100000
   "num_invalid_format": 0,
   "num_invalid_user": 0,
   "num_invalid_segment": 0,
   "num_unauth_segment": 1,
   "num_past_expiration": 0,
   "num_inactive_segment": 0,
   "num_other_error": 0,
   "error_log_lines": " \n\nnum_unauth_segment-4013681496264948522;5013:0,5014:1550",
   "segment_log_lines": "\n5010:100000\n5011:50000\n5012:50000",
   "id": 88,
   "job_id": "4tGhzv2PojNGQpq0MYaoaOa70cuF061337630675",
   "member_id": 456,
   "created_on": "2012-05-21 20:04:35",
   "last_modified": "2012-05-21 20:08:24"
  },
  "dbg_info": {
  ...
  },
  "status": "OK",
  "num_elements": 100
 }
}
```

## Possible upload errors

### Attempting to upload file larger than 0.5GB

```
{"response":{"status":"ERROR","error_code":"FILESIZE_LIMIT_EXCEEDED","errors":["Member
exceeds maximum byte size allowed for a file"]}}
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

The following are errors that may happen when:

- You've canceled the upload
- The upload phase exceeds 90 minutes
- You've reached one of its four upload limits (daily bytes, hourly bytes, or hourly lines limit)

### Attempting to exceed daily byte upload limit

```
{"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
exceeds maximum allowed bytes per day"]}}
```

### Attempting to exceed hourly byte upload limit

```
{"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
exceeds maximum allowed bytes per hour"]}}
```

### Attempting to exceed daily lines upload limit

```
{"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
exceeds maximum allowed number of lines per day"]}} 
```

### Attempting to exceed hourly lines upload limit

```
{"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Member
exceeds maximum allowed lines per hour"]}}
```

### Exceeding maximum time to upload

```
{"response":{"status":"ERROR","error_code":"RATE_LIMIT_EXCEEDED","errors":["Maximum
upload time exceeded"]}}
```

## Possible processing errors

### Invalid format

If the value of the `num_invalid_format` field is greater than `"0"`, check the values in the `error_log_lines` field (see **Example** below). Note the following in the `error_log_lines` field:

- `num_invalid_format` indicates there was a problem parsing a line in the uploaded file.

- `"failed with an illegal number of fields"` indicates that the number of fields in a `segment_fields` block did not match what was defined in the batch-segment config (see [Initial BSS Account Setup](initial-bss-account-setup.md) for more information). In the below example, the config indicates three fields: `SEG_ID`, `VALUE`, `EXPIRATION`, but the parser only found two fields: `SEG_ID`, `VALUE`

    ```
    segment_fields: [SEG_ID,VALUE,EXPIRATION]
    ```

#### `num_invalid_format` and `error_log_lines` example

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

To see metadata about all of your segment file uploads within the last 30 days, make a `GET` call to the service with your `member_id` specified in the query string. The JSON response will include an array of `batch_segment_upload_job` objects. For more information about the specific fields of the `batch_segment_upload_job` object, see [JSON Fields](#json-fields).

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
> ```
> &start_element=101
> ```
>
> ```
> &sort=last_modified.desc
> ```
>
> You can read more about pagination in [Throttling, Pagination, and Filtering](../digital-platform-api/05---throttling-pagination-and-filtering.md).

## JSON fields

> [!TIP]
> To find out which fields you can filter and sort by, make a GET call to `https://api.appnexus.com/batch-segment/meta`.

| Fields | Type | Description |
|---|---|---|
| `batch_segment_upload_job` | object | The object whose fields contain metadata describing the upload and processing job. If you are using the Impbus API, this will be an array containing a single object. See [Batch Segment Upload Job](#batch-segment-upload-job) below for details. |
| `id` | int | This is the ID of the `batch_segment_upload_job` object associated with this request. <br><br> **Default**: An automatically generated number. |
| `status` | string | The status of the API call; successful calls return `"OK"`. |

### Batch segment upload job

When you request the status of your processing job, the system returns a `batch_segment_upload_job` object (if you are a data provider, this will be an array containing a single object). Depending upon which request you're making to the service, it will contain some or all of the following metadata. For more information about the required sequence of requests, see [Add a Segment File for Processing](#add-a-segment-file-for-processing) below.

> [!NOTE]
> Most metadata will only be present when `"phase" = "completed."`

| Fields | Type | Description |
|---|---|---|
| `completed_time` | date | The time at which file processing was completed. |
| `created_on` | date | The creation date of this object. |
| `error_code` | int | If `"phase" = "error"`, this error code describes the type of error encountered. Note that an error code will only be shown here if there was an error with the uploading, validating, or processing of the file itself (i.e. does not include invalid format or invalid segment errors). Common errors are caused by unreadable files and exceeding defined object limits. Returns `null` if no errors were found. |
| `error_log_lines` | string | A string containing newline-separated lines. Each line lists a validation error or the reason for an error while uploading your file. You can choose how many lines (200 by default) appear in this field. |
| `id` | int | The unique identifier of this object. |
| `job_id` | string | A string of alphanumeric characters that uniquely identifies the processing job associated with this file. |
| `last_modified` | date | The most recent modification date of this object (usually via `POST`). |
| `member_id` | int | Your member ID. |
| `num_inactive_segment` | int | The number of inactive segments in the file. Deduplicated. |
| `num_invalid_format` | int | The number of uploaded lines containing formatting errors (This depends upon your particular file format configuration). Duplicate lines will also be considered to be an invalid format. |
| `num_invalid_segment` | int | The number of invalid segments in the file. Deduplicated. |
| `num_invalid_timestamp` | int | The number of invalid timestamps in the file. |
| `num_invalid_user` | int | This is a count of unique input lines that have an invalid or nonexistent user |
| `num_other_error` | int | This is a placeholder value not currently in use. |
| `num_past_expiration` | int | The number of expired segments in the file. Deduplicated. |
| `num_unauth_segment` | int | The number of segments in the file which you are unauthorized to access. Deduplicated. |
| `num_valid` | int | The number of valid lines in the uploaded file. Each user/segment combination is considered 1 line. |
| `num_valid_user` | int | This is a count of unique input lines that have a valid user ID. |
| `percent_complete` | int | The percentage of the processing that has been completed, given the current `phase` at the time of the request. |
| `phase` | enum | The current processing status, one of `"error"`, `"starting"`, `"uploading"`, `"validating"`, `"processing"`, or `"completed"`. |
| `segment_log_lines` | string | A string containing newline-separated lines. Each line lists a segment and how many users were successfully added to it. This field defaults to 200 lines. |
| `start_time` | date | The time at which file upload began. |
| `time_to_process` | decimal | How long it took to process the segment file, in minutes. |
| `upload_url` | string | The URL where you'll upload your segment data file. |
| `uploaded_time` | date | The time at which the file associated with this job ID was uploaded. |
| `validated_time` | date | The time at which file validation was completed. |

## Related topic

[Batch Segment Service - Sample PHP Script](legacy-bss-file-format.md)
