---
title: Member Data Sharing Service - Sample PHP Scripts
description: In this article, learn about the sample PHP scripts for the member data sharing service with a detailed set of examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Member data sharing service - Sample PHP scripts

The following scripts will help you interface with the member-data-sharing service. These scripts will help you:

> [!NOTE]
> This sample code serves as a guideline for partners and is not actively serviced by Xandr.

## Scripts for viewing records

### List existing sharing records

This script will print the list of `buyer_member_ids` that you are currently sharing data with and their respective `record_ids`.

```
<?
$PROD_URL = "https://api.adnxs.com"; // for impression bus API logins
//$PROD_URL = "https://api.appnexus.com"; // for API logins
$api_url = $PROD_URL;
$api_username = ""; // your API login
$api_password = ""; // your API password
$member_id = -9999; // your member ID
// login and authentication
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
$result = curl_exec($ch);
// Call function to grab sharing ids
get_sharing_ids($ch, $api_url, $member_id);
//================================================================================================================
//   Function: get_sharing_ids                                                                                   =
//   Inputs:   $ch - curl handler, $api_url - API URL endpoint, $member_id - your member id                      =
//   Purpose:  Purpose of this function is to parse the response from a GET to the                               =
//             member data sharing service and print the buyer members and their respective sharing record ids.  =
//================================================================================================================
function get_sharing_ids($ch, $api_url, $member_id) {
  echo "\nHitting API Service: ".$api_url."/member-data-sharing?data_member_id=".$member_id."\n\n";
  curl_setopt($ch, CURLOPT_URL, $api_url."/member-data-sharing?data_member_id=".$member_id);
  curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
  $response = curl_exec($ch);
  $response_obj = json_decode($response);
  for($i = 0; $i < count($response_obj->response->member_data_sharings); $i++) {
    print "Member ID: ".$response_obj->response->member_data_sharings[$i]->buyer_member_id."\t\tSharing Record ID: ".$response_obj->response->member_data_sharings[$i]->id."\n";
  }
}
?>
        
```

### View segments shared in existing sharing record

The following script takes in a record ID and prints the segments shared in that sharing record.

```
<?
if ($argc < 2) {
  die("Please provide a record id!\n");
 } else {
  $record_id = $argv[1];
 }
$PROD_URL = "https://api.adnxs.com"; // for impression bus API logins
//$PROD_URL = "https://api.appnexus.com // for API logins
$api_url = $PROD_URL;
$api_username = ""; // your API login
$api_password = ""; // your API password
$member_id = -9999; // your member ID
// login and authentication
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
$result = curl_exec($ch);
// retrieve sharing record
curl_setopt($ch, CURLOPT_URL, $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
$response = curl_exec($ch);
$response_obj = json_decode($response);
// Print shared segments
if ($response_obj->response->member_data_sharing->segment_exposure == 'all') {
  print "Sharing all segments in record ".$record_id."\n\n";
}
else {
  for($i = 0; $i < count($response_obj->response->member_data_sharing->segments); $i++) {
    print "segment_id: ".$response_obj->response->member_data_sharing->segments[$i]->id."\tName: ".$response_obj->response->member_data_sharing->segments[$i]->name."\n";
  }
}
?>
      
```

## Scripts for adding to existing records

### Add single segment to an existing sharing record

The following script takes in a specific record ID and segment ID and adds the segment ID to that record.

```
<?
if ($argc < 3) {
  die("Please provide a record id and a segment id!\n");
 } else {
  $record_id = $argv[1];
  $segment->id = $argv[2];
 }
$PROD_URL = "https://api.adnxs.com"; // for impression bus API logins
//$PROD_URL = "https://api.appnexus.com // for API logins
$api_url = $PROD_URL;
$api_username = ""; // your API login
$api_password = ""; // your API password
$member_id = -9999; // your member ID
// login and authentication
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
$result = curl_exec($ch);
// Retrieve existing sharing record
curl_setopt($ch, CURLOPT_URL, $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
$response = curl_exec($ch);
$response_obj = json_decode($response);
// Append the new segment_id to existing segment_id array
$segment_array = array();
$segment_array = $response_obj->response->member_data_sharing->segments;
array_push($segment_array, clone($segment));
// PUT updated segment array through the API
$put_obj->member_data_sharing->segments = $segment_array;
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PUT");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($put_obj));
$response = curl_exec($ch);
print "\n".$response."\n";
print $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id."\n";
?>
      
```

### Add list of segments to existing sharing record

This script adds a list of segments to an existing sharing record. The script takes in as input the `record_id` as well as the `file_name` where the list of `segment_ids` is saved. The script expects that the file be formatted as list of comma separated values.

```
<?
if ($argc < 3) {
  die("Please provide a record id and a segment id!\n");
 } else {
  $record_id = $argv[1];
  $segment_file = $argv[2];
 }
$PROD_URL = "https://api.adnxs.com"; // for impression bus API logins
//$PROD_URL = "https://api.appnexus.com // for API logins
$api_url = $PROD_URL;
$api_username = ""; // your API login
$api_password = ""; // your API password
$member_id = -9999; // your member ID
// login and authentication
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
$result = curl_exec($ch);
// Retrieve existing sharing record
curl_setopt($ch, CURLOPT_URL, $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
$response = curl_exec($ch);
$response_obj = json_decode($response);
// Open segment file and create array of segments to append
$fh = fopen($segment_file, 'r');
$segment_data = fread($fh, filesize($segment_file));
fclose($fh);
$seg_array = explode(",", $segment_data);
// Append to existing segment array
$segment_array = array();
$segment_array = $response_obj->response->member_data_sharing->segments;
for($i = 0; $i < count($seg_array); $i++) {
  $segment->id = $seg_array[$i];
  array_push($segment_array, clone($segment));
}
// PUT updated segment array through the API
$put_obj->member_data_sharing->segments = $segment_array;
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PUT");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($put_obj));
$response = curl_exec($ch);
print "\n".$response."\n";
print $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id."\n";
?>
```

## Scripts for deleting records

### Delete a single segment from a sharing record

This script takes in as inputs the `record_id` and the `segment_id` and deletes the `segment_id` from that `record_id`. You can use this script in conjunction with a bash script to delete that specific segment from multiple records at once.

```
<?
if ($argc < 3) {
  die("Please provide a record id and a segment id!\n");
 } else {
  $record_id = $argv[1];
  $segment->id = $argv[2];
 }
$PROD_URL = "https://api.adnxs.com"; // for impression bus API logins
//$PROD_URL = "https://api.appnexus.com // for API logins
$api_url = $PROD_URL;
$api_username = ""; // your API login
$api_password = ""; // your API password
$member_id = -9999; // your member ID
// login and authentication
$ch = curl_init();
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_COOKIEFILE, "cookies.txt");
curl_setopt($ch, CURLOPT_COOKIEJAR, "cookies.txt");
curl_setopt($ch, CURLOPT_URL, $api_url."/auth?username=".$api_username."&password=".$api_password);
$result = curl_exec($ch);
// Retrieve existing sharing record
curl_setopt($ch, CURLOPT_URL, $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "GET");
$response = curl_exec($ch);
$response_obj = json_decode($response);
// Extract segments array
$segment_array = array();
$segment_array = $response_obj->response->member_data_sharing->segments;
// Find the index of the delete segment
$delete_index = binary_search($segment_array, 0, count($segment_array), $segment, "compare");
// Create new array without the delete segment
unset($segment_array[$delete_index]);
$segment_array = array_values($segment_array);
// PUT updated segment array through the API
$put_obj->member_data_sharing->segments = $segment_array;
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "PUT");
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($put_obj));
$response = curl_exec($ch);
print "\n".$response."\n";
print $api_url."/member-data-sharing?data_member_id=".$member_id."&id=".$record_id."\n";
// Implement binary_search for finding segment to delete
function binary_search($segment_array, $first, $last, $search_segment, $compare) {
  $lo = $first;
  $hi = $last - 1;
  while($lo <= $hi) {
    $mid = (int)(($hi - $lo)/2) + $lo;
    $cmp = call_user_func($compare, $segment_array[$mid]->id, $search_segment->id);
    if ($cmp < 0) {
      $lo = $mid + 1;
    }
    elseif ($cmp > 0) {
      $hi = $mid - 1;
    }
    else {
      return $mid;
    }
  }
  return -($lo + 1);
}
function compare($a, $b) {
  if ($a == $b) {
    return 0;
  }
  return ($a < $b) ? -1 : 1;
}
?>
```
