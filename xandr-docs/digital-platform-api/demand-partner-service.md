---
title: Demand Partner Service
description: Use the Demand Partner service to return all demand partners for the caller's member.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Demand Partner service

The Demand Partner Service returns all demand partners for the caller's member. It enables the user to create a new demand partner and update or delete an existing demand partner.

In the context of PSP, demand partners, usually supply-side platforms (SSPs) like, create adapters for Prebid Server that receive and interpret header bidding ad requests. Demand partners hold an auction among their demand sources (usually demand-side-platforms (DSPs)) to collect bids on those ad requests and send the bids back to PSP, which holds another auction.

Before a demand partner can be added to a configuration, they must be enabled via this service or [through the UI](../monetize/add-or-edit-a-demand-partner.md). Setting a demand partner to `enabled: false` pauses all bid requests to that partner across all configurations until the setting is restored to `true`. The list of demand partners compatible with PSP [can be found here](../monetize/prebid-server-premium-demand-partner-integrations.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/prebid/demand-partner` | Get all demand partners. |
| `POST` | `https://api.appnexus.com/prebid/demand-partner` | Create a new demand partner. |
| `PUT` | `https://api.appnexus.com/prebid/demand-partner/{id}` | Update an existing demand partner. |
| `PATCH` | `https://api.appnexus.com/prebid/demand-partner/{id}` | Update a portion of an existing demand partner. |
| `DELETE` | `https://api.appnexus.com/prebid/demand-partner/{id}` | Delete a demand partner. |

## `GET`

Get all or a specific demand partner. To retrieve a specific demand partner, append the demand partner ID as last component of the URL path. Returns a JSON array of demand partner objects.

### Response

| Property | Type | Description |
|:---|:---|:---|
| `bid_cpm_adjustment` | integer | A multiplier value applied to the Demand Partner's CPM bid price to adjust how the bids compete in auction. This does not change the actual bid or revenue payout, only the ranking of the bid in the auction. The default value is 1.00. In this case all partners' bids compete equally with no adjustments. The adjustment can be used to account for partner fees or for optimization. If you need CPM adjustments at a level more granular than Demand Partner, see [Create a Bias Rule](../monetize/create-a-bias-rule.md). |
| `deleted` | boolean | This indicates that the demand partner object has been deleted from the system. |
| `enabled` | boolean | Indicates if the demand partner is enabled or disabled. |
| `id` | integer | The demand partner ID specific to the caller's member. |
| `last_modified` | string | The date that the demand partner object was modified. |
| `last_modified_by` | string | The user who last modified the demand partner object. |
| `member_id` | integer | The member ID. |
| `name` | string | The name of the demand partner. |
| `pub_id_settings` | object | The options relevant to the publisher-provided user IDs. See the [publisher provided ID settings](#publisher-provided-id-settings) table below. |

### Publisher provided ID settings

| Property | Type | Description |
|:---|:---|:---|
| `id` | integer | Unique identifier representing the source. |
| `source` | string | Unique string representing the source. |
| `member_owner_id` | integer | Unique identifier of the member that owns the source. |
| `status` | string | Indicates if the source is active. Requires string input of `"active"` or `"inactive"`. |

#### Example response

```
[
    {
        "bid_cpm_adjustment": 2,
        "deleted": false,
        "enabled": true,
        "id": 102,
        "last_modified": "2019-09-13T17:39:36Z",
        "last_modified_by":"user123",
        "member_id": 9325,
        "name": "adform",
        "pub_id_settings": {
            "sources": [
                {
                    "id": 12345,
                    "source": "sourcename",
                    "member_owner_id": 9325,
                    "status": "active"
                }
            ]
        }
    },
    {
        "bid_cpm_adjustment": 1,
        "deleted": false,
        "enabled": true,
        "id": 65,
        "last_modified": "2018-11-02T15:33:54Z",
        "last_modified_by":"user123",
        "member_id": 9325,
        "name": "appnexus",
        "pub_id_settings": null
    },
    {
        "bid_cpm_adjustment": 1,
        "deleted": false,
        "enabled": true,
        "id": 68,
        "last_modified": "2018-11-02T18:32:03Z",
        "last_modified_by":"user123",
        "member_id": 9325,
        "name": "openx",
        "pub_id_settings": null
    },
    {
        "bid_cpm_adjustment": 1,
        "deleted": false,
        "enabled": true,
        "id": 69,
        "last_modified": "2018-11-02T18:32:31Z",
        "last_modified_by":"user123",
        "member_id": 9325,
        "name": "ix",
        "pub_id_settings": null
    }
]
```

## POST

Create a new demand partner.

### Example call using curl

```
curl -d @demand-partner.json -X POST 'https://api.appnexus.com/prebid/demand-partner'
```

| Property | Type | Scope | Description |
|:---|:---|:---|:---|
| `bid_cpm_adjustment` | integer | Required | The bid CPM adjustment. |
| `enabled` | boolean | Required | Indicates if the demand partner is enabled or disabled. |
| `name` | string | Required | The name of the demand partner. |
| `pub_id_settings` | object | Required | The options relevant to the publisher-provided user ids. See [publisher provided ID settings table](#publisher-provided-id-settings) above. |

### Example JSON

```
{
    "bid_cpm_adjustment": 1,
    "enabled": true,
    "name": "test-demand-partner",
    "pub_id_settings": {
        "sources": [
            {
                "id": 12345,
                "source": "sourcename",
                "member_owner_id": 9325,
                "status": "active"
            }
        ]
    }
}
```

### Response

A successful response will return the new demand partner as a JSON object.

```
{
    "bid_cpm_adjustment": 1,
    "deleted": false,
    "enabled": true,
    "id": 999,
    "last_modified": "2020-02-25T18:32:31Z",
    "last_modified_by":"user123",
    "member_id": 9325,
    "name": "test-demand-partner",
    "pub_id_settings": {
        "sources": [
            {
                "id": 12345,
                "source": "sourcename",
                "member_owner_id": 9325,
                "status": "active"
            }
        ]
    }
}
```

## PUT

Updates an existing Prebid demand partner. Include the id as last component of the path. Pass the update information as JSON in the body of the request.

### Example call using curl

```
curl https://api.appnexus.com/prebid/demand-partner/1234
```

### JSON example

```
{
    "id": 1234,
    "name": "openx",
    "enabled": 0,
    "bid_cpm_adjustment": 1,
    "pub_id_settings": null
  }
```

### Response

Returns updated Prebid demand partner object.

## PATCH

Partially update an existing Prebid demand partner. Include the ID as last component of the path. Pass the update information as JSON in the body of the request.

```
{
    "enabled": 0,
    "bid_cpm_adjustment": 1
}
```

### Example call using curl

```
curl https://api.appnexus.com/prebid/demand-partner/1234
```

### Response

Returns the updated Prebid demand partner object.

## DELETE

Delete an existing Prebid demand partner. Include the ID as last component of the path.

### Example call using curl

```
curl https://api.appnexus.com/prebid/demand-partner/1234
```

### Response

The success response of the Prebid demand partner object is returned as a JSON object with the deleted property set to true. The Prebid demand partner will no longer be available in the system. Any sub-objects will also be deleted.

## Managing identity sources

> [!NOTE]
>
> - Each identifier source must have permission at the Microsoft member, bidder (Prebid Server Premium, ID 443), and demand partner level in order to successfully pass through in requests to demand partners.
> - For more information on the identifier registration process and managing identifiers, review the [Identity Service API](./identity-service.md).
> - In the future, the Identity Management UI will allow for holistic management of identifier permissions.
> - This service currently is in Alpha. It is still under development and may be subject to change without notice. Contact your Microsoft Account Representative to get enabled.

## Related topics

- [Demand Partner Schema Service](./demand-partner-schema-service.md)
- [Prebid Demand Partner Params Service](./prebid-demand-partner-params-service.md)
- [PSP Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md)
- [Add or Edit a Demand Partner](../monetize/add-or-edit-a-demand-partner.md)
- [Prebid Server Premium Identity & User Syncing](../monetize/prebid-server-premium-identity-and-user-syncing.md)
- [Identity Service](./identity-service.md)
