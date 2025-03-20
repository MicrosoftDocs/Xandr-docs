---
title: Prebid Demand Partner Params Service
description: Explore the Prebid Demand Partner Params service to manage specific partners on PSP configurations by adding, removing, enabling, disabling, and viewing them.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Prebid Demand Partner Params service

The Prebid Demand Partner Params Service allows users to view, add, remove, enable, and disable specific partners on PSP configurations. Configurations are managed via the [Config Service](config-service.md). A demand partner must be enabled in the [Cross-Partner Settings Service](../digital-platform-api/cross-partner-settings-service.md) before they can be added to any configurations in the params service and before they can receive bid requests through Prebid Server Premium (PSP). Attempting to add a partner who is not present in the Cross-Partner Settings will result in an error.

> [!NOTE]
> While a partner may be disabled via this service at the configuration level, any future changes to the partner in the [Cross-Partner Settings Service](cross-partner-settings-service.md) will override individual configurations and enable/disable the partner across all configurations. Details on the parameters supported by each partner can be found in the [Demand Partner Schema Service](demand-partner-schema-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | - [https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}](https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}) | Get all Prebid demand partner parameters for a specific Prebid configuration. |
| `GET` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Get a specific Prebid demand partner parameter. Include the `param ID` as the last URL path component. |
| `POST` | [https://api.appnexus.com/prebid/prebid-demand-partner-params](https://api.appnexus.com/prebid/prebid-demand-partner-params) | Create new demand partner parameters. For cURL example and response, see [`POST`](#post) section below. |
| `PUT` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Update a specific Prebid demand partner parameter. Include the `param ID` as the last component of the URL path. |
| `DELETE` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Delete a specific Prebid demand partner parameter. Include the `param ID` as the last URL path component. |

## `GET`

Returns all or a specific set of demand partner parameters within a PSP configuration. Include either the `prebid_settings_id` (configuration) or the ID of the parameters as the last component of the URL.

### Example call using cURL to return a specific param

```

curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}

```

### Example call using cURL to return all params for a specific config

```

curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}

```

### Response

A successful response will return all parameters for the requested Prebid configuration or a specific requested parameter.

| Property | Type | Description |
|:---|:---|:---|
| `deleted` | boolean | Indicates whether the params object for this partner has been deleted. |
| `enabled` | boolean | Indicates if the demand partner is enabled or disabled via the [demand partner service](demand-partner-service.md). |
| `id` | integer | The unique identifier for the set of parameters associated with the demand partner in the PSP configuration. |
| `last_modified` | string | The most recent modification date of the demand partner config params. |
| `last_modified_by` | string | The person who made the last modifications to the demand partner params. |
| `member_id` | integer | The caller's member ID. |
| `name` | object | The name of the demand partner. |
| `params` | object | An object containing the parameters supported by the partner and the mapped values. Supported parameters can be found [here](demand-partner-schema-service.md). |
| `prebid_settings_id` | integer | The unique identifier of the PSP configuration. |

### Response example

```
[
  {
    "id": 1718542,
    "member_id": 13859,
    "prebid_settings_id": 196038,
    "name": "appnexus",
    "params": {
      "placement_id": 123456
    },
    "enabled": 0,
    "deleted": 0,
    "last_modified_by": "user123",
    "last_modified": "2024-08-22T21:45:05.000Z"
  }
]         
            
```

## `POST`

Enables the creation of a new Prebid Demand Partner Param object. The `enabled` field must not be included in any requests to this service. The value is inherited from the status of the partner in the [demand partner service](demand-partner-service.md).

### Example call using cURL

```
curl -d @demand-partner-params.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/prebid-demand-partner-params'
```

#### Example JSON request

```
{
    "prebid_settings_id": 196038,
    "member_id": 13859,
    "name": "adform",
    "params": {
        "inv": null,
        "mid": "11111111",
        "mname": null,
        "priceType": null
    }
}
```

### Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the Prebid demand partner. |
| `member_id` | integer | Required |  The ID of the member associated with the configuration. |
| `params` | object | Required | An object containing the parameters supported by the partner and the mapped values. Supported parameters can be found [here](demand-partner-schema-service.md). |
| `prebid_settings_id` | integer | Required | The unique identifier for the PSP configuration.|

### `POST`: Example response

```
[
  {
    "id": 1718543,
    "member_id": 13859,
    "prebid_settings_id": 196038,
    "name": "adform",
    "params": {
      "inv": null,
      "mid": "11111111",
      "mname": null,
      "priceType": null
    },
    "enabled": 1,
    "deleted": 0,
    "last_modified_by": "user123",
    "last_modified": "2024-08-22T22:40:21.000Z"
  }
]       
```

## `PUT`

Overwrites an existing Prebid demand partner parameter. Include the `prebidDemandPartnerParamId` as the last component of the URL path. Pass the update information as JSON in the body of the request. The `enabled` field must not be included in any requests to this service. The value is inherited from the status of the partner in the [demand partner service](demand-partner-service.md).

### `PUT`: Example call using cURL

```
curl -d @config-update.json -X PUT --header "Content-Type: application/json https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}
```

### Example JSON request

```
{
    "member_id": 13859,
    "prebid_settings_id": 196038,
    "name": "adform",
    "params": {
        "inv": null,
        "mid": "11111111",
        "mname": null,
        "priceType": null
    }
}
```

### `PUT`: Response

Returns a Prebid demand partner param object.

## `DELETE`

Delete an existing Prebid demand partner param. Include the `prebidSettingsId` as the last component of the path.

### `DELETE`: Example call using cURL

```
curl -X DELETE https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}
```

### `DELETE`: Response

On success the Prebid demand partner param object is returned as a JSON object with the deleted property set to true. The Prebid demand partner params will no longer be available in the system. Any sub-objects will also be deleted.

## Related topics

- [Demand Partner Service](demand-partner-service.md)
- [Demand Partner Schema Service](demand-partner-schema-service.md)
- [Config Service](config-service.md)
- [PSP Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md)
- [Add or Edit a Demand Partner](../monetize/add-or-edit-a-demand-partner.md)
- [Add, Edit, or Delete a PSP Configuration](../monetize/add-edit-or-delete-a-psp-configuration.md)
