---
title: Deal List Service
description: Deal List service facilitates search and fetching a specific or different deal lists. You can create, append and replace a deal list with comma-separated deal IDs.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Deal List service

A deal is an agreement between a buyer and a seller that provides special access to inventory and/or data. Deals are primarily used to access preferred premium inventory or negotiated inventory. A deal list is a group of deals IDs categorised under a heading for targeting across line items. Deal lists allow inventory specialists to curate deals inventory for traders as well as streamline trader workflows like targeting the same set of deals across line items. If deal grouping requirements change, only making required changes in the deal list will automatically update all line items accordingly.

Deal List API facilitates search, add, modify, and fetching a specific or different deal lists. It allows you to create, append and replace a deal list with comma-separated deal IDs.

> [!NOTE]
> All query parameters in Deal List service support a list of comma separated values. For example, to delete a set of deal lists, a comma separated list of IDs can be passed as query parameters.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/deal-list`<br>(Deal List JSON) | Add a new deal list. |
| `PUT` | `https://api.appnexus.com/deal-list`<br>(Deal List JSON) | Modify a deal list. |
| `DELETE` | `https://api.appnexus.com/deal-list?id=DEAL_LIST_ID` | Delete a deal list. |
| `DELETE` | `https://api.appnexus.com/deal-list?id=DEAL_LIST_ID1,DEAL_LIST_ID2,DEAL_LIST_ID3` | Delete different deal lists. |
| `GET` | `https://api.appnexus.com/deal-list` | View all deal lists and deals they contain. |
| `GET` | `https://api.appnexus.com/deal-list?name=DEAL_LIST_NAME` | View a deal list by name and deals it contain. |
| `GET` | `https://api.appnexus.com/deal-list?id=DEAL_LIST_ID` | View a specific deal list and deals it contain. |
| `GET` | `https://api.appnexus.com/deal-list?advertiser_id=ADVERTISER_ID` | View a deal list by advertiser id and deals it contain. |
| `GET` | `https://api.appnexus.com/deal-list?deal_id=DEAL_ID` | View all deal lists containing a deal. |
| `GET` | `https://api.appnexus.com/deal-list?search=SEARCH_TERM`<br><br>**Note**:<br>`SEARCH_TERM` may be `DEAL_ID` or `DEAL_LIST_NAME` containing certain characters. | Search a deal list by ID or name as search term. |
| `GET` | `https://api.appnexus.com/deal-list?search=SEARCH_TERM&advertiser_id=ADVERTISER_ID`<br><br>**Note**:<br>`SEARCH_TERM` may be `DEAL_ID` or `DEAL_LIST_NAME` containing certain characters. | Search a deal list by ID or name as search term and accessible to a particular advertiser. |
| `GET` | `https://api.appnexus.com/deal-list?line_item_id=LINE_ITEM_ID` | View all deal lists targeted by a line item. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of a deal list.<br><br>**Required On**: `PUT`, in the JSON payload. |
| `name` | string | The name of the deal list.<br><br>**Required On**: `POST`, in the JSON payload. |
| `deals` | array of objects | The deals that are to be included in the deal list. The deal IDs of the deals are included here. See [Example for this field](#example-for-the-deals-field). <br><br>**Required On**:`POST`, `PUT` |
| `advertisers` | array of objects | The advertisers for whom the deal list is meant for. The advertiser IDs are included here. See [Example for this field](#example-for-the-advertisers-field). <br><br>**Note**:<br>On `POST` calls, if the `advertisers` field is either set to an empty array or set without any value, it defaults to all the advertisers to whom the user has access to. In other words, if the user has access to all the advertisers under a member, this field defaults to an empty array because there is no advertiser specific restriction present.<br><br>Similarly on `PUT` calls, if the advertisers are set to empty arrays, it defaults to all advertisers to whom the user has access to (not setting a field value on `PUT` calls have no effect). |
| `last_modified` | timestamp | Time of last modification made to the deal list.<br><br>**Read Only**. |
| `created_on` | timestamp | Time of creation of the deal list. |
| `line_items` | array of objects | The line items that are targeting the deal list (line items that have a profile attached to them and that profile is targeting the deal list). See [Example for this field](#example-for-the-line_items-field).<br><br>**Read Only**. |

### Example for the `deals` field

```
"deals":[
{"id":1},
{"id":2},
{"id":3}
],
```

### Example for the `advertisers` field

```
"advertisers":[
{"id":1},
{"id":2},
{"id":3}
],
```

### Example for the `line_items` field

```
"line_items":[
{"id":1,
"name":"LINE_ITEM1",
"code":null
},
{
"id":2,
"name":"LINE_ITEM2",
"code":null
}
],
```

## Examples

### Create a deal list

In this example, we create a new deal list.

```
$ cat deal-list-create
 
{ 
   "deal-list":[ 
      { 
         "name":"My first deal list",
         "description": null,
         "advertisers":[
            {"id": 1},
            {"id": 2},
            {"id": 3}
         ]
      },
      { 
         "deals":[ 
            {"id": 1},
            {"id": 2},
            {"id": 3}
         ],
         "name":"Another one"
      }
   ]
}
 
$ curl -b cookies -X POST -d @deal-list-create 'https://api.appnexus.com/deal-list'
 
{
    "response": {
        "status": "OK",
        "deal-list": {
           "id": 3901,
           "name": "My first deal list"
           ....
         }
    }
}
```

### Update a deal list

In this example, we update a deal list.

```
$ cat deal-list-update
 
{ 
   "deal-list": { 
       "deals": [{"id": 1}],
       "name":"My modified first deal list",
       "id":3901
   }
}
 
$ curl -b cookies -X PUT -d @deal-list-update 'https://api.appnexus.com/deal-list'
 
{
    "response": {
        "status": "OK",
        "inventory-list": {
           "id": 3901,
           "name": "XYZ Allowlist"
           "description": "Updated Description",
           ....
         }
    }
}
```

### Delete a deal list

In this example, we delete an existing deal list.

```
$ curl -b cookies -c cookies -X DELETE https://api.appnexus.com/deal-list?id=3901
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

- [Profile Service](./profile-service.md)
- [Splits Service](./splits-service.md)
