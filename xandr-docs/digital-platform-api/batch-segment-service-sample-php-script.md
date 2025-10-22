---
title: Batch Segment Service - Sample PHP Script
description: In this article, find a sample PHP script for the Batch Segment Service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Batch Segment Service - Sample PHP script

> [!NOTE]
>
> - This service is currently available to a limited set of clients and Microsoft employees only.
> - The content on this page is provided only as an example; we cannot robustly support PHP script implementations with clients.

The following script will connect to the Batch Segment Service, request a job ID and upload URL, `POST` your segment file to the upload URL, and return yet another URL where you can check the status of your processing job.

It accepts one argument: the filename of your segment data file.

```
<?php
if ($argc < 2) {
  die("No File Name Specified!\n");
} else {
  $filename = $argv[1];
}
// Edit with user-specific details
$api_url = "sand.api.appnexus.com"; // for appnexus logins
//$api_url = 'hb.sand-08.adnxs.net'; // for adnxs logins
$api_username = "username"; // your API login
$api_password = 'password'; // your API password
$member_id = 0; // your member ID
// login
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
curl_exec($ch);
// Send post request to batch-segment
curl_setopt($ch, CURLOPT_URL, $api_url."/batch-segment?member_id=".$member_id);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
//Get the upload URL
$response = curl_exec($ch);
$response_obj = json_decode($response);
$upload_url=$response_obj->response->batch_segment_upload_job->upload_url;
$job_id=$response_obj->response->batch_segment_upload_job->job_id;
//Send the file to the unique URL
exec("curl -v -H 'Content-Type:application/octet-stream' --data-binary @".$filename." '".$upload_url."'");
//Exec this command to see your job status
echo("\ncurl -b cookies -c cookies '".$api_url."/batch-segment?member_id=".$member_id."&job_id=".$job_id."'\n");
?>
```
