---
title: Geo Polygon Segment Service
description: Use the Geo Polygon Segment service to create, configure, and export geo polygon segments.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Geo Polygon Segment service

> [!NOTE]
> This service is in **Alpha**. This feature is subject to change without notice and is only available to select clients. If you would like to participate in the Alpha test, please contact your account manager.

The Geo Polygon Segment Service lets you create, configure, and export geo polygon segments. A geo polygon segment is a list of user locations specified by Well-known text (WKT) polygon coordinates. Well-known text (WKT) is a text markup language for representing vector geometry objects on a map using coordinates. After you create a geo polygon segment, you can use the segment automatically associated with it for geographical targeting of multiple user locations. The Geo Polygon Segment Service lets you to upload CSV files of geo polygon WKT into a geo segment. You can use the same geo segment for targeting at the line item level.

> [!WARNING]
> Geo Polygon Segment Service is based on Well-known text (WKT) polygon coordinates. This indicates that the geo polygons must be uploaded in **longitude and latitude (long, lat)** format instead of latitude and longitude (lat, long) format.

## Process flow

To create a segment with geo polygons, follow below steps:

1. Create a shell segment. To create the shell segment, make a POST call to the **`/geo-polygon-segment`** endpoint.
1. Upload polygons to the shell segment. You can create a CSV file with polygons in it and make a POST call to the **`/geo-polygon-segment/{segmentID}/upload-polygon`** endpoint.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/geo-polygon-segment`<br><br>(new-geo-polygon-segment JSON) | Create a new geo polygon segment |
| `POST` | `https://api.appnexus.com/geo-polygon-segment/{segmentID}/upload-polygon`<br><br>(add-polygons.csv) | Add polygons to a segment |
| `POST` | `https://api.appnexus.com/geo-polygon-segment`<br><br>(new-geo-polygon-segment JSON) | Create a new geo polygon segment |
| `POST` | `https://api.appnexus.com/geo-polygon-segment/select`<br><br>`POST -d '{"criteria":{},"ordering": {"direction":"desc","by":"id"}}' "https://api.appnexus.com/geo- polygon-segment/select"` | View all geo polygon segments for a member |
| `POST` |`https://api.appnexus.com/geo-polygon-segment/{segmentID}/polygon/select`<br><br>`POST -d '{"criteria":{},"ordering":{"direction":"desc","by":"id"}}' "https://api.appnexus.com/geo-polygon-segment/{segmentID}/polygon/select"` | View a specific geo polygon segment's details |
| `POST` |`https://api.appnexus.com/geo-polygon-segment/{segmentID}/polygon/select`<br><br>`POST -d '{"criteria":{},"ordering":{"direction":"desc","by":"id"}}' "https://api.appnexus.com/geo-polygon-segment/{segmentID}/polygon/select"` | View all geo polygon definitions in a segment |
| `GET` | `https://api.appnexus.com/apd-status` | View recent uploads |
| `GET` | `https://api.appnexus.com/apd-status?id=%7Bapd_id%7D` | View status of a specific upload |
| `GET` | `https://api.appnexus.com/geo-segment-processor/job-status` | View status of a geo polygon upload |
| `DELETE` | `https://api.appnexus.com/geo-polygon-segment/{segmentID}` | Delete a geo polygon segment |
| `DELETE` | `https://api.appnexus.com/geo-polygon-segment/%7BsegmentID%7D/polygon/delete`<br><br>`POST -d '{"criteria":{"id":{"in":[_polygon_feature_id_]}}}' "https://api.appnexus.com/geo-polygon-segment/{segmentID}/polygon/delete"` | Delete a specific feature from a geo polygon segment |

## JSON fields

### Create new geo polygon segment JSON

| Field | Type | Description |
|:---|:---|:---|
| `code` | string | User-defined code for calling the geo polygon segment. For example, `"GEO123"` |
| `description` | string | Description for this geo polygon segment |
| `short_name` | string | Short name used to describe the geo polygon segment<br><br>**Required On**: `POST` |
| `regional_centers` | array of objects | ID or code of the region in which the geo polygon segment is available.<br>**Possible values:**<br> - `ID: 1, 2 or 3`<br> - `code: "americas", "emea", "apac"` |

### `CSV` file format

The CSV file has the column names as **Polygon** and **Name** and they hold the values for the defined geo-polygons.

> [!NOTE]
> Column names are case-sensitive and without any space. You must specify the column names in your CSV file.

#### Example

##### `add-polygons.csv`

```
Polygon,Name
"POLYGON((-73.79619781688602 40.926119268030504,-73.96923248485477 40.95931402310335,-74.09008209422977 
40.52648176879785,-73.23864166454227 
40.62870062738066,-73.38421051219852 40.926119268030504,-73.79619781688602 40.926119268030504))",FirstPolygon
```

> [!NOTE]
> The polygons must be specified inside quote marks, as required by the CSV file standard.

Once you upload the CSV file successfully, the API sends response with below fields:

- `geo_segment_polygon_id`: The auto-generated ID of the geo polygon as stored in Xandr's system.
- `name`: The name of the geo-polygon.
- `apd_id`: The job ID of the upload. You must keep track of this in case you want to track down the status of the upload.

> [!NOTE]
> You need to keep record of the upload responses as it will be necessary for troubleshooting.

## Examples

### Create a new geo polygon segment

```
$ cat new-geo-polygon-segment.json

{
  "short_name": "New Geo Polygon Segment",
  "description": "Creating a new geo polygon segment example",
  "regional_centers": [
    {
      "id": 1
    }
  ]
}

Alternatively

$ cat new-geo-polygon-segment.json
{
  "short_name": "New Geo Polygon Segment",
  "description": "Creating a new geo polygon segment example",
  "regional_centers": [
    {
      "code": "emea"
    }
  ]
}

$ curl -b cookies -d @new-geo-segment.json -X POST "https://api.appnexus.com/geo-polygon-segment"
{
 "id": 35619,
 "segment_id": 27258480,
 "created_on": "2021-08-04 03:17:41",
 "updated_on": "2021-08-04 03:17:41"
}
```

### View all supported regional centers

```
$ curl -b cookies "https://api.appnexus.com/regional-center"
{
 "regional_centers": [
   {
     "id": 1,
     "code": "emea",
     "name": "Europe, Middle East, Africa"
   },
  {
     "id": 2,
     "code": "americas",
     "name": "North, Central and South America"
  },
  {
     "id": 3,
     "code": "apac",
     "name": "Asia and Pacific"
  }
 ]
}
```

### Upload polygons to the newly created segment

```
$ curl -b cookies -c cookies -X POST --form 'file=@"/home/add-polygons.csv"' "https://api.appnexus.com/geo-polygon-
segment/27258480/upload-polygon"

[
    {
    "geo_segment_polygon_id": 47,
    "name": "FirstPolygon"
    }
    {
    "apd_id": "393cc786-f537-11eb-b5b0-3cfdfedf9b61"
    }
]
```

### View all geo polygon segments for a member

```
$ curl -b cookies -c cookies -X POST -d '{"criteria":{},"ordering":{"direction":"desc","by":"id"}}' 
"https://api.appnexus.com/geo-polygon-segment/select"
```

### View all geo polygon definitions in a segment

```
curl -b cookies -c cookies -X POST -d '{"criteria":{},"ordering":{"direction":"desc","by":"id"}}' 
"https://api.appnexus.com/geo-polygon-segment/27258480/polygon/select"
```

### View recent uploads

```
curl -b cookies "https://api.appnexus.com/apd-status"
```

### View status of a specific upload

```
curl -b cookies "https://api.appnexus.com/apd-status?id=4d362ab8-f94d-11eb-a5ee-3cfdfec8e950"
```

### View upload status of geo polygon upload

```
curl -b cookies -c cookies -X GET "https://api.appnexus.com/geo-segment-processor/job-status?geoSegmentId=86831"
```

### Delete a geo polygon segment

```
curl -b cookies -c cookies -X DELETE "https://api.appnexus.com/geo-polygon-segment/27258480"
```

### Delete a specific feature from a geo polygon segment

```
curl -b cookies -c cookies -X POST -d 
 '{"criteria":
    {"id":
      {"in":[9653092]}
    }
  }' 
"https://api.appnexus.com/geo-polygon-segment/31584260/polygon/delete" | json_reformat
```

## Important points to note

- The Geo Polygon Segment Service does not currently accept geo polygon definitions with holes (In geometry, a polygon with holes is an area-connected planar polygon with one external boundary and one or more interior boundaries). If a polygon definition contains a hole, the service will ignore the hole.
- The maximum number of polygon definitions that can be hosted in a segment is 50,000.
- When the uploading of the CSV file is successful, the service returns `apd_id` and `geo_segment_polygon_id` in response. You need to save them for any troubleshooting in future.
- If uploaded file has some issues such as invalid formatting, missing quotes, trailing spaces, segment already having 50000 polygon definitions etc., then there would not be any `geo_segment_polygon_id` in the response. If the upload response contains only `apd_id`, that signifies that file was rejected due to any of the reasons mentioned above. In such cases, it is recommended to rectify the issue and attempt the upload again.
- Multi-polygons are not supported currently. Please split multi-polygon definitions into unique, individual, polygon definitions and upload only those.
- A geo polygon segment can be connected to a maximum of one regional centre.
