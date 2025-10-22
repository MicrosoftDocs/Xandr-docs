---
title: Admin Log-Level Report
description: Learn the process to use the Admin Log-Level report in order to run select queries for log-level data.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Admin Log-Level report

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Admin Log-Level Report (aka Honeycomb) gives Xandr admins an easy and safe way to run **select** queries for log-level data. This page walks you through the process.

> [!NOTE]
> This report is currently in **alpha** phase. Feel free to use internally, but dependence on this service for client deliverables is not advisable.

## Step 1. Create a JSON-formatted report request

The JSON-formatted file must include three fields:

- `report_type` - Set this field to `"admin_backdoor_hive"`.
- `hostname` - Set this field to `"hd_quest_internal"`.
- `sql` - This field should contain the **select** query that you want to run against a hive view. Other types of queries, such as insert, update, and create, are not supported.

> [!NOTE]
> - If a request takes more than 6 minutes, it will be stopped. Therefore, please specify the narrowest scope possible for your query (see below for an example).
> - Make sure to filter your results by dh and not datetime! If you filter by datetime, hive will pull the entire log to disk, not only the hour you're searching.
> - Lastly, remember that most logs are only retained for 3 days.

```
$ cat honeycomb
{
    "report": {
        "report_type": "admin_backdoor_hive",
        "hostname": "hd_quest_internal",
        "sql": "select auction_id_64, tag_id, imp_type, buyer_bid from view_log_impbus_impressions where dh >= '2013-09-17 00' and dh <= '2013-09-17 01' limit 25"
    }
    }
```

## Step 2. `POST` the request to the report service

You `POST` the JSON request and get back a `report_id`.

```
$ curl -b cookies -c cookies -X POST -d @honeycomb 'https://api.appnexus.com/report'
                   {
                   "response": {
                   "status": "OK",
                   "report_id": "727d8ac797dbd2f4fcdf1b5b3dfacc78",
                   "dbg_info": {
                   "instance": "33.bm-hbapi.prod.ams1",
                   "s1ave_hit": false,
                   "db": "master",
                   "awesomesauce_cache_used": false,
                   "warnings": [
                   ],
                   "time": 1092.3848152161,
                   "start_microtime": 1366149528.4808,
                   "version": "1.13.24"
                   }
                   }
                   }
```

## Step 3. `GET` the report status from the report service

Make a `GET` call with the report ID to retrieve the status of the report. Continue making this `GET` call until the `execution_status` is `"ready"`.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/report?id=7d346f7371479ccd9df3e963d328b111'
                   {
                   "response": {
                   "status": "OK",
                   "report": {
                   "name": null,
                   "created_on": "2013-04-16 22:01:36",
                   "cache_hit": true,
                   "fact_cache_hit": false,
                   "fact_cache_error": null,
                   "json_request": "{\"report\":{\"report_type\":\"admin_backdoor_hive\",\"hostname\":\"hd_quest_internal\",\"sql\":\"select * from view_log_impbus_impressions where dh >= '2013-04-15 00' and dh <= '2013-04-15 23' limit 25\",\"columns\":[\"null\"]}}",
                   "header_info": null,
                   "row_count": null,
                   "report_size": null,
                   "internal_info": "{\"report_id\":\"16b4abe25279c12d8ec35663f4ffcd2d\",\"cache_hit_using\":\"84e157f95a9ae491bae87a88413a6107\",\"controller_cache_hit\":true}",
                   "user_id": "1432",
                   "entity_id": "0",
                   "started_on": "0000-00-00 00:00:00",
                   "finished_on": "2013-04-16 22:01:37",
                   "query_time": null,
                   "url": "report-download?id=727d8ac797dbd2f4fcdf1b5b3dfacc78"
                   },
                   "execution_status": "ready",
                   "dbg_info": {
                   "instance": "07.hbapi.sand-08.lax1",
                   "s1ave_hit": false,
                   "db": "master",
                   "awesomesauce_cache_used": false,
                   "warnings": [
                   ],
                   "time": 73.494911193848,
                   "start_microtime": 1366149711.5471,
                   "version": "1.13.24.5"
                   }
                   }
                   }
```

> [!NOTE]
> **Advanced Debugging**
>
> If you feel the need to debug your request or see metadata about the file containing your results (size, path, errors, etc.), you can make the following query in mysql:
>
> ```
> select * from bidder.report where id=<id>' and 'select * from bidder.report_data where id=<id>
> ```

## Step 4. `GET` the report data from the report download service

To download the report data, make another `GET` call with the Report ID, but this time to the `report-download` service. You can find the service and Report ID in the `url` field of the previous `GET` response.

> [!NOTE]
> If an error occurs during download, the response header may include an HTTP error code an message. Use `-i` or `-v` in your call to expose the response header.

```
$ curl -i -b cookies -c cookies 'https://api.appnexus.com/report-download?id=727d8ac797dbd2f4fcdf1b5b3dfacc78'
                 HTTP/1.1 200 OK
                 Date: Fri, 19 Apr 2013 14:19:44 GMT
                 Server: Apache
                 Expires: Thu, 19 Nov 1981 08:52:00 GMT
                 Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
                 Pragma: no-cache
                 Content-Length: 855
                 X-Cnection: close
                 Content-Type: text/html; charset=UTF-8
                 6483826219503747324     1146450 6       0.2001
                 8757791008875425961     1243542 6       0.056495
                 3138296207856430744     1063554 5       0.23
                 8309764363038038757     1177460 2       0.0
                 7661919662664341200     1176566 2       0.0
                 3196824821514784768     1176603 2       0.0
                 508831754820345939      1177539 1       0.0
                 1502106846291195018     1177483 2       0.0
                 2375712734375133632     817633  6       2.25
                 752197030132686720      1177632 2       0.0
                 1213486872149318238     1273605 4       0.0
                 3415859912223023849     449971  4       0.0
                 6263040305047094681     1177441 1       0.0
                 2121733891987323973     1176566 2       0.0
                 6997147601954947287     1200128 5       0.4
                 7306230783443618843     1177447 2       0.0
                 6266523220830097933     750026  5       0.011587
                 405012229025485566      1177561 2       0.0
                 8263566825993015008     1177471 1       0.0
                 49544838857644841       1177460 2       0.0
                 6843928551867445242     1178060 2       0.0
                 161715005479869174      1177439 1       0.0
                 6592596437155421974     749840  5       0.09
                 7301110445143310330     1177457 2       0.0
                 2531722883911340869     837015  4       0.0
```
