---
title: Postal Code List Service
description: Explore the features of Postal Code List service, enabling users to search, create, fetch, and delete a specific postal code list.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Postal Code List service

In the traditional way of geo-targeting audiences, users can target only a limited number of postal codes at the line item or split level. With the introduction of the Postal Code List Service API into the Xandr platform, this limitation will be eliminated. The Postal Code List API will allow buyers to create a list of postal codes and reuse it across different objects (line items, splits) for targeting. With the Postal Code List Service, users can now target 100k postal codes on an individual list and 100 individual lists on a line item or split.

The Postal Code List service enables users to:

- Search, create, fetch, and delete a specific or different postal code list, include and exclude postal code lists containing a number of postal codes (by postal code ID).
- Enable include and exclude postal code list targeting on the line item and split level.

> [!IMPORTANT]
>
> - The maximum number of postal codes lists allowed per member is 8,000.
> - Postal code lists that have not been modified in six months and are not associated with line items that have served in the last six months are eligible to be deleted by Xandr.
> [!NOTE]
> All query parameters in the postal code list service support a list of comma-separated values. For example, to delete a set of postal code lists, a comma-separated list of IDs can be passed as query parameters.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/postal-code-list](https://api.appnexus.com/postal-code-list) | Add a new Postal Code List. |
| `PUT` | [https://api.appnexus.com/postal-code-list](https://api.appnexus.com/postal-code-list) | Modify a Postal Code List. |
| `DELETE` | [https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID](https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID) | Delete a Postal Code List. |
| `DELETE` | [https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID1,POSTAL_CODE_LIST_ID2,POSTAL_CODE_LIST_ID3](https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID1,POSTAL_CODE_LIST_ID2,POSTAL_CODE_LIST_ID3) | Delete multiple Postal Code Lists. |
| `GET` | [https://api.appnexus.com/postal-code-list](https://api.appnexus.com/postal-code-list) | View all Postal Code Lists and Postal Codes they contain. |
| `GET` | [https://api.appnexus.com/postal-code-list?name=POSTAL_CODE_LIST_NAME](https://api.appnexus.com/postal-code-list?name=POSTAL_CODE_LIST_NAME) | View a Postal Code List by name and Postal Codes it contains. |
| `GET` | [https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID](https://api.appnexus.com/postal-code-list?id=POSTAL_CODE_LIST_ID) | View a specific Postal Code List and Postal Codes it contains. |
| `GET` | [https://api.appnexus.com/postal-code-list?postal_code_id=POSTAL_CODE_ID](https://api.appnexus.com/postal-code-list?postal_code_id=POSTAL_CODE_ID) | View all Postal Code Lists containing a Postal Code. |
| `GET` | [https://api.appnexus.com/postal-code-list?search=SEARCH_TERM](https://api.appnexus.com/postal-code-list?search=SEARCH_TERM) | Search a Postal Code List by ID or name as search term.<br><br>**Note:**<br>`SEARCH_TERM` may be `POSTAL_CODE_ID` or `POSTAL_CODE_LIST_NAME` containing certain characters. |
| `GET` | [https://api.appnexus.com/postal-code-list?line_item_id=LINE_ITEM_ID](https://api.appnexus.com/postal-code-list?line_item_id=LINE_ITEM_ID) | View all Postal Code Lists targeted by a line item. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of a postal code list.<br>**Required On:** `PUT` |
| `name` | string | The name of the postal code list.<br>**Required On:** `POST` |
| `postal_codes` | array of objects | The postal codes that are to be included in the postal code list. The postal code IDs of the postal codes are included here. For example, see the [formats](#postal_codes-formats) that can be used.<br><br>**Note:**<br>For the USA, you can target the full 9-digit postal code (also known as zip +4). For example, see [below](#postal_codes-example).<br><br> **Required On:** `POST` and `PUT`. |
| `advertiser_ids` | array of objects | **Optional**. Indicates which advertisers have access to the Postal Code List (PCL). This field will allow associating one or multiple advertisers with the PCL. A maximum of 50 advertisers is allowed per PCL. If the `advertiser_ids` field is not specified, by default, the PCL is open to all advertisers.<br>For example, see [below](#advertiser_ids-example). |
| `last_modified` | timestamp | Time of the last modification made to the postal code list.<br>It's a **Read Only** field. |
| `created_on` | timestamp | Time of creation of the postal code list.<br>It's a **Read Only** field. |
| `line_items` | array of objects | The line items that are targeting the postal code list (line items that have a profile attached to them and that profile is targeting the postal code list).<br>It's a **Read Only** field.<br>For example, see [below](#line_items-example). |

### `postal_codes` formats

```
"postal_codes":[
{"id": 1},
{"id": 2},
{"id": 3}
],
```

```
"postal_codes": [
{"country_code":"US","code":"10010"},
{"country_code":"US","code":"10111"},
{"country_code":"US","code":"10100"}
],
```

### `postal_codes` example

```
"postal_codes":[{"country_code":"US","code":"10010-7456"}],
```

### `advertiser_ids` example

**API JSON with the optional `advertiser_ids` field:**

```
{
   "postal-code-lists":[
      {
         "postal_codes":[
            {"id": 1},
            {"id": 2},
            {"id": 3}
         ],
         "name":"My first postal code list"
         "advertiser_ids":[
            {"id": 1},
            {"id": 2},
            {"id": 3}
         ] 
      }
   ]
}
```

**Example response:**

```
{
    "response": {
        "status": "OK",
        "count": 2,
        "id": 169386,
        "start_element": 0,
        "num_elements": 100,
        "postal-code-list": {
            "id": 169386,
            "code": null,
            "name": "My first postal code list",
            "description": null,
            "created_on": "2023-08-14 15:36:17",
            "last_modified": "2023-08-14 15:36:17",
            "postal_codes_count": 1,
            "postal_codes": [
                {
                    "id": 1,
                    "code": "00010",
                    "country_id": 113,
                    "active": true,
                    "country_code": "IT",
                    "country_name": "Italy"
                },
                {
                    "id": 2,
                    "code": "00010",
                    "country_id": 113,
                    "active": true,
                    "country_code": "IT",
                    "country_name": "Italy"
                },
                {
                    "id": 3,
                    "code": "00010",
                    "country_id": 113,
                    "active": true,
                    "country_code": "IT",
                    "country_name": "Italy"
                }
            ],
            "line_items": null,
            "advertiser_ids":[
               {"id": 1}, {"id": 2}, {"id": 3}
            ], 
        },
        "dbg_info": {
            "warnings": [],
            "version": "1.2.216",
            "output_term": "postal-code-list"
        }
    }
}
```

### `line_items` example

```
"line_items":[
{
"id" : 1,
"name": "LINE_ITEM1",
"code": null
},
{
"id" : 2,
"name": "LINE_ITEM2",
"code": null
}
],
```

## Examples

### Create a postal code list

```
$ cat postal-code-list-create

{
   "postal-code-lists":[
      {
         "postal_codes":[
            {"id": 1},
            {"id": 2},
            {"id": 3}
         ],
         "name":"My first postal code list"
      },
      {
         "postal_codes": [ 
            {"country_code":"US","code":"10011"},
            {"country_code":"US","code":"10110"},
            {"country_code":"US","code":"11111"}
        ],
         "name":"Another one"
      }
   ]
}

$ curl -b cookies -X POST -d @postal-code-list-create 'https://api.appnexus.com/postal-code-list'
{
    "response": {
        "status": "OK",
        "postal-code-list": {
           "id": 3901,
           "name": "My first postal code list"
           ....
         }
    }
}
```

### Update a postal code list

```
$ cat postal-code-list-update

{
    "postal-code-list": {
        "id": 3901,
        "name": "Modified Postal Code List name",
        "description": "Modified Postal Code List description",
        "postal_codes": [
            {"id": 2}
        ]
    }
}

$ curl -b cookies -X PUT -d @postal-code-list-update 'https://api.appnexus.com/postal-code-list'
{
    "response": {
        "status": "OK",
        "postal-code-list": {
           "id": 3901,
           "name": "modified postal code list name"
           "description": "Updated Description",
           ....
         }
    }
}
```

### Add a new postal code to postal code list

```
$ cat postal-code-list-update

{
    "postal-code-list": {
        "id": 3901,
        "postal_codes": [
            {"id": 9987}
        ]
    }
}

$ curl -b cookies -X PUT -d @postal-code-list-update 'https://api.appnexus.com/postal-code-list&append=true'

{
    "response": {
        "status": "OK",
        "postal-code-list": {
           "id": 3901,
           "postal_codes": [
            {"id": 9987}
        ]
    }
}
```

### Delete a postal code list

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/postal-code-list?id=3901'

{
    "response": {
        "status": "OK",
        "count": 1,
        "start_element": null,
        "num_elements": null
    }
}
```

## Related topics

- [Profile Service](profile-service.md)
- [Splits Service](splits-service.md)
