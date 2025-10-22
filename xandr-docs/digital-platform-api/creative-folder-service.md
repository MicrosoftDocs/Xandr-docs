---
title: Creative Folder Service
description: In this article, learn about the Creative Folder service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Creative Folder service

The creative folder service allows you to group creatives for organizational purposes. You can add multiple creatives at once to a folder as you create it.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID) | View all creative folders (you must specify advertiser). |
| `GET` | [https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID&id=FOLDER_ID](https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID&id=FOLDER_ID) | View a specific creative folder. |
| `POST` | [https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID)<br>(creative-folder JSON) | Add a new creative folder (you can add creatives to the folder in this action or afterwards). |
| `POST` | [https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID)<br>(creative-folder JSON) | Add a new creative to one of your folders. |
| `PUT` | [https://api.appnexus.com/creative-folder?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/creative-folder?id=CREATIVE_ID&advertiser_id=ADVERTISER_ID)<br>(creative-folder JSON) | Modify an existing creative folder. |
| `DELETE` | [https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID&id=FOLDER_ID](https://api.appnexus.com/creative-folder?advertiser_id=ADVERTISER_ID&id=FOLDER_ID) | Delete an existing creative folder. |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `id` | int | The internal ID associated with the creative folder. |
| `parent_id` | int | **Deprecated.** |
| `name` | string | The optional name for the creative folder. |
| `advertiser_id` | int | All creatives are attached to either an advertiser or publisher at the time of creation. |
| `creatives` | array of objects | List of creatives you wish to include in this folder, or list of creatives already in the folder, depending on your request. |
| `last_modified` | timestamp | The date and time when the creative folder was last modified. |

## Examples

### Add a creative folder that contains two (pre-existing) creatives

```
{code}$ cat creative-folder

{
    "creative-folder":{
        "creatives":[{
                "id":246305
            },
            {
                "id":246221
            }
        ]
    }
}

$ curl -b cookies -c cookies -X POST -d @creative-folder 'https://api.appnexus.com/creative-folder?advertiser_id=493'

{
  "response": {
    "status": "OK",
    "id": 338
  }
}
{code}
```

### View all folders for advertiser 493

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-folder?advertiser_id=493'

{
  "response": {
    "creative-folders": [
      {
        "id": 81,
        "parent_id": null,
        "advertiser_id": 493,
        "name": "Hosted Images",
        "last_modified": "2010-03-31 21:26:59",
        "creatives": [
          {
            "id": "14900"
          }
        ]
      },
      {
        "id": 82,
        "parent_id": null,
        "advertiser_id": 493,
        "name": "3rd party images",
        "last_modified": "2010-03-31 21:27:07",
        "creatives": [
          {
            "id": "246305"
          }
        ]
      },
      {
        "id": 152,
        "parent_id": null,
        "advertiser_id": 493,
        "name": "an-creatives-2",
        "last_modified": "2010-08-05 15:18:50",
        "creatives": [
          {
            "id": "246214"
          },
          {
            "id": "246215"
          },
          {
            "id": "246216"
          },
          {
            "id": "246217"
          },
          {
            "id": "246218"
          },
          {
            "id": "246219"
          },
          {
            "id": "246220"
          },
          {
            "id": "246221"
          }
        ]
      },
      {
        "id": 338,
        "parent_id": null,
        "advertiser_id": 493,
        "name": null,
        "last_modified": "2011-06-20 19:15:18",
        "creatives": [
          {
            "id": "246221"
          },
          {
            "id": "246305"
          }
        ]
      }
    ],
    "status": "OK",
    "count": 4,
    "start_element": 0,
    "num_elements": 100
  }
}
{code}
```

### Add a creative to an existing creative folder

Be sure to include `append=true` to your query statement. If you leave this off, all existing creatives in the folder will be overwritten.

```
$ cat creative-folder

{
    "creative-folder":{
        "creatives":[{
                "id":876543
            }
        ]
    }
}

curl -b cookies -X PUT -d @creative-folder 'https://api.appnexus.com/creative-folder?id=338&advertiser_id=493&append=true'

{
  "response": {
    "status": "OK",
    "id": 338
  }
}
```
