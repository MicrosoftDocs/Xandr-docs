---
title: Deal Buyer Setting Service
description: Learn about the Deal Buyer Setting service. It allows buyers to give deals an alias and assign a status, giving them more control.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Deal Buyer Setting service

The Deal Buyer Setting Service lets buyers give deals an internal alias for clarity in the UI and assign a status to deals so buyers have more control over which deals they’re targeting. Note that these deal settings are only available to the buyers who created them and are not visible to the seller of the deal.

> [!NOTE]
> Buyers can use the [Deal Buyer Access Saervice](./deal-buyer-access-service.md) to view the deals available to them and the `deal_targets`field in the [Profile Service](./profile-service.md) to target them. Sellers can use the [Deal Service](./deal-service.md) to set up and manage deals.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/deal-buyer-setting` | View all of your deal settings. |
| `GET` | `https://api.appnexus.com/deal-buyer-setting?id=ID` | View a specific deal setting. |
| `GET` | `https://api.appnexus.com/deal-buyer-setting?deal_id=DEAL_ID` | View the settings for a specific deal. |
| `GET` | `https://api.appnexus.com/deal-buyer-setting?id=1,2,3` | View multiple deal settings by ID using a comma-separated list. |
| `GET` | `https://api.appnexus.com/deal-buyer-setting/meta` | Find out which fields you can filter and sort by. |
| `POST` | `https://api.appnexus.com/deal-buyer-setting` | Add settings for a deal. |
| `PUT` | `https://api.appnexus.com/deal-buyer-setting?id=ID` | Modify settings for a deal. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `acceptance_status` | string | The status of the deal: <br> - `active` <br> - `inactive` <br> - `declined` <br> - `pending`<br><br>**Note**: `pending` status is not allowed in a `PUT` request<br><br>**Default**: The default for this field depends on the value of the `member.default_accept_deals` field (see [Member Service](./member-service.md)). If `member.default_accept_deals` is `true`, the default for `acceptance_status` is `active`; if `member.default_accept_deals` is `false`, the default for `acceptance_status` is `pending`. |
| `buyer_bidder_id` | int | The bidder ID of the member. For buyers, this will always be `2`.<br><br>**Read Only**<br>**Default**: `null` |
| `buyer_member_id` | int | The ID of the member who can buy the deal. A deal will either be set up with a buyer member ID or a buyer seat code. This is your Xandr member ID.<br><br>**Read Only** |
| `buyer_seat_code` | string | The code of the buyer seat who can buy the deal. A deal will either be set up with a buyer member ID or a buyer seat code. This is your Xandr member ID.<br><br>**Read Only**<br>**Default**: `null` |
| `comments` | string (65534) | **Not yet being used by the UI**. The custom comments to display in the UI for the deal.<br><br>**Default**: `null` |
| `deal_id` | int | The ID of the deal to which the settings apply.<br><br>**Required On**: `POST` |
| `deal_alias` | string (254) | The alias of the deal, as it will appear in the UI.<br>**Default**: `null` |
| `id` | int | The ID of the deal settings<br><br>**Required On**: `PUT`<br>**Default**: auto-incremented number. |

## Examples

### Add deal setting

If a deal-buyer-setting object has already been created for the deal, the POST request will return the following error message: "`The buyer_member_id, deal_id combination was not unique.`" To modify this deal-buyer-setting, first make a `GET` `https://api.appnexus.com/deal-buyer-setting?deal_id=DEAL_ID` request to return the deal-buyer-setting ID. Then use the deal-buyer-setting ID with a `PUT` `https://api.appnexus.com/deal-buyer-setting?id=ID` request to modify the deal-buyer-setting.

```
$ cat deal_settings.json
 
{
    "deal-buyer-setting": {
        "deal_id": 22896,
        "deal_alias": "This is an alias",
        "comments": "this is a comment on a deal",
        "acceptance_status": "active"
    }
}

$ curl -b cookies -c cookies -X POST -d @deal_settings.json 'https://api.appnexus.com/deal-buyer-setting'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "12005",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-setting": {
            "id": 12005,
            "deal_id": 22896,
            "deal_alias": "This is an alias",
            "comments": "this is a comment on a deal",
            "buyer_member_id": 546,
            "acceptance_status": "active"
        }
    }
}
```

### Modify deal settings

```
$ cat deal_settings_update.json
 
{
    "deal-buyer-setting": {
        "deal_alias": "new deal alias"
    }
}

$ curl -b cookies -c cookies -X PUT -d @deal_settings_update.json 'https://api.appnexus.com/deal-buyer-setting?id=11777'
 
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": "11777",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-setting": {
            "id": 11777,
            "deal_id": 560402,
            "deal_alias": "new deal alias",
            "comments": null,
            "buyer_member_id": 546,
            "acceptance_status": "active"
        }
    }
}
```

### View all of your deal settings

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-setting'
 
{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-settings": [
            {
                "id": 9980,
                "deal_id": 558605,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            },
            {
                "id": 10950,
                "deal_id": 559575,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            },
            {
                "id": 11777,
                "deal_id": 560402,
                "deal_alias": "new deal alias",
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            }, 
            {
                "id": 1802,
                "deal_id": 550427,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            },
            {
                "id": 1937,
                "deal_id": 550562,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            }
        ]
    }
}
```

### View the settings for a specific deal settings ID

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-setting?id=11777'

{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-settings": [
            {
                "id": 11777,
                "deal_id": 560402,
                "deal_alias": "new deal alias",
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            }
        ]
    }
}
```

### View the settings for a specific deal ID

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-setting?deal_id=560402'

{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-settings": [
            {
                "id": 11777,
                "deal_id": 560402,
                "deal_alias": "new deal alias",
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            }
        ]
    }
}
```

### View the settings for multiple deal IDs

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/deal-buyer-setting?deal_id=560402,559575,558605'

{
    "response": {
        "status": "OK",
        "start_element": 0,
        "num_elements": 100,
        "deal-buyer-settings": [
            {
                "id": 9980,
                "deal_id": 558605,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            },
            {
                "id": 10950,
                "deal_id": 559575,
                "deal_alias": null,
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            },
            {
                "id": 11777,
                "deal_id": 560402,
                "deal_alias": "deal alias",
                "comments": null,
                "buyer_member_id": 546,
                "acceptance_status": "active"
            }
        ]
    }
}
```
