---
Title : Uploading Segment Data Using BSS
Description : As described in this document, adding your segment file to the system is
a multi-step process.
---


# Uploading Segment Data Using BSS



As described in this document, adding your segment file to the system is
a multi-step process.

- Step 1: <a
  href="https://docs.xandr.com/bundle/xandr-api/page/uploading-segment-data-using-bss.html#UploadingSegmentDataUsingBSS-Formatyourdatafileforupload"
  class="xref" target="_blank">Format your data file for upload</a>.
- Step 2: <a
  href="https://docs.xandr.com/bundle/xandr-api/page/uploading-segment-data-using-bss.html#UploadingSegmentDataUsingBSS-RequestanuploadURLandjobID"
  class="xref" target="_blank">Request an upload URL and Job ID</a>.
- Step 3: <a
  href="https://docs.xandr.com/bundle/xandr-api/page/uploading-segment-data-using-bss.html#UploadingSegmentDataUsingBSS-PostthefiletotheuploadURL"
  class="xref" target="_blank">Post the file to the upload URL</a>.
- Step 4: <a
  href="https://docs.xandr.com/bundle/xandr-api/page/uploading-segment-data-using-bss.html#UploadingSegmentDataUsingBSS-Checkthejobstatus"
  class="xref" target="_blank">Check the job status</a>.

<div id="buy-side-service-template__note_ldb_hpw_5wb"


Note: Files are limited to 1800
segments on any individual line. If you have more than 1800 segments for
one user, you must break that line into multiple lines.



<div id="buy-side-service-template__UploadingSegmentDataUsingBSS-Formatyourdatafileforupload"
>

## Format your data file for upload

You have two options when creating a data file for BSS: the <a
href="https://docs.xandr.com/bundle/xandr-api/page/legacy-bss-file-format.html"
class="xref" target="_blank">Legacy BSS File Format</a> and the
**newer**, **preferred** <a
href="https://docs.xandr.com/bundle/xandr-api/page/bss-avro-file-format.html"
class="xref" target="_blank">BSS Avro File Format</a>, which uses a
self-defined schema and supports a wider range of IDs beyond third-party
cookies.

Note that your data file must meet the following requirements:

- Uses the
  <a href="http://en.wikipedia.org/wiki/ISO/IEC_8859-1" class="xref"
  target="_blank">Latin1</a> character set.
- Is a maximum of 0.5GB.



<div id="buy-side-service-template__UploadingSegmentDataUsingBSS-RequestanuploadURLandjobID"
>

## Request an upload URL and job ID

Each segment data file that is uploaded must be associated with a
particular job ID. This ID is used to create the upload URL and to track
the file's processing status. The first step is to send an empty `POST`
request to the service.

This service works for both
<a href="https://api.appnexus.com/" class="xref"
target="_blank">api.appnexus.com</a> and for
<a href="http://api.adnxs.com/" class="xref"
target="_blank">api.adnxs.com</a>. It is available for both bidder and
UI logins.

``` pre
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
      "upload_url": "https://data-api-gslb.adnxs.net/segment-upload/segment-upload/JFY8l6iMOFAFJIWCMPcy39MCt3Yleo1337618549"
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



<div id="buy-side-service-template__UploadingSegmentDataUsingBSS-PostthefiletotheuploadURL"
>

## Post the file to the upload URL

The file upload URL is given in the JSON response in Step 1 by the field
upload_url: you will `POST` your segment file to this URL for
processing. Keep the following guidelines in mind:

- Do not hard-code the upload URL in your application. Make sure to
  dynamically grab it from the upload_url field.
- You must begin your upload to the given Upload URL within five (5)
  minutes, and only one URL is valid at any given time. If you wait
  longer than 5 minutes to start your upload, you must request a new
  URL.
- We recommend, you do not exceed one upload per minute. If you have
  more than 200 jobs waiting to be processed at any given time, you will
  be prohibited from uploading additional jobs.

<div id="buy-side-service-template__note_shb_4pw_5wb"
class="note warning note_warning">

Warning: To upload the file correctly,
you must specify the MIME type in the HTTP header as
`"Content-Type: application/octet-stream"`*.* Don't use
`"Content-Type: application/x-www-form-urlencode"`

( `-d or --data flags in curl`). Using an incorrect MIME type will
prevent the file from being processed.



``` pre
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

**Example of SSL upload URL**

``` pre
curl -b cookie -c cookie -X POST -s -d '' "https://api.appnexus.com/batch-segment?member_id=958"
 
"batch_segment_upload_job": {
      "id": 14841671,
      "job_id": "qGQhSZ1qvd2hSsJ9svTz32qgxq7z5b1439315424",
      "member_id": 958,
      "last_modified": "2015-08-11 17:50:24",
      "upload_url": "https://data-api-gslb.adnxs.net/segment-upload/qGQhSZ1qvd2hSsJ9svTz32qgxq7z5b1439315424"
      }
```



<div id="buy-side-service-template__UploadingSegmentDataUsingBSS-Checkthejobstatus"
>

## Check the job status

Finally, check the processing status by sending a GET request with the
`job_id` returned from step 2 or 3. The JSON response contains
information such as how long the file took to process and the number of
errors, if any. Note that you should wait until phase="completed" before
looking at the results fields such as `num_valid`. For more detailed
information, see <a
href="https://docs.xandr.com/bundle/xandr-api/page/troubleshooting-bss-uploads.html"
class="xref" target="_blank">Troubleshooting BSS Uploads</a>.

Per Xandr SLA, allow up to 24 hours for the file to process.

<div id="buy-side-service-template__note_zlh_fqw_5wb"


Note: If you are a data provider using
the Impbus API, note that the `batch_segment_upload_job`



field will be an array with a single object inside of it. For example,

``` pre
{"batch_segment_upload_job":[{"phase":"completed" }]}
```





``` pre
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






