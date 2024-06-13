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
| `GET` | [https://api.appnexus.com/prebid/prebid-demand-partner-params](https://api.appnexus.com/prebid/prebid-demand-partner-params) | Get all Prebid demand partner configs. |
| `GET` | - [https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}](https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id})<br>- [https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}&member_id={member_id}](https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}&member_id={member_id}) | Get all Prebid demand partners for a specific Prebid setting. |
| `GET` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Get a specific Prebid demand partner config. Include the `prebidSettingsId` as the last URL path component. |
| `POST` | [https://api.appnexus.com/prebid/prebid-demand-partner-params](https://api.appnexus.com/prebid/prebid-demand-partner-params) | Create new demand partner parameters. For cURL example and response, see [`POST`](#post) section below. |
| `PUT` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Update an existing Prebid demand partner config. |
| `DELETE` | [https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}](https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}) | Delete a specific Prebid demand partner config. Include the `prebidSettingsId` as the last URL path component. |

## `GET`

Returns all or a specific Prebid demand partner config params for the caller's member. For a specific Prebid demand partner config include the `prebidSettingsId` as the last URL path component. Results are returned as JSON.

### Example call using cURL to return a specific config

Append the config ID as the last component of the URL.

```
curl --header "Content-Type: application/json" https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidSettingsId}
```

### Return all Prebid Demand Partner Config Params for a specific prebid setting

```
GET https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}
 
//or 

GET https://api.appnexus.com/prebid/prebid-demand-partner-params?prebid_settings_id={prebid_settings_id}&member_id={member_id}
```

### Response

A successful response will return JSON containing all the Prebid configs for the member or the requested Prebid config.

| Property | Type | Description |
|:---|:---|:---|
| `deleted` | boolean | Indicates whether the params object for this partner has been deleted. |
| `enabled` | boolean | Indicates if the Prebid demand partner params are enabled or disabled. |
| `id` | integer | The caller's ID. |
| `last_modified` | string | The most recent modification date of the demand partner config params. |
| `last_modified_by` | string | The person who made the last modifications to the demand partner params. |
| `member_id` | integer | The caller's member ID. |
| `name` | object | The name of the demand partner. |
| `params` | object | An object containing the parameters supported by the partner and the mapped values. Supported parameters can be found [here](demand-partner-schema-service.md). |
| `prebid_settings_id` | integer | The Prebid setting object's ID. |

### Response example

```
[
   {
      "id":104,
      "prebid_settings_id":30,
      "name":"improvedigital",
      "member_id":7293,
      "params":{
         "size":null,
         "keyValues":null,
         "placementId":567594,
         "publisherId":null,
         "placementKey":null
      },
      "enabled":true,
      "deleted":false,
      "last_modified_by":"test123",
      "last_modified":"2019-09-03T22:48:58.135Z"
   }
]            
            
```

## `POST`

Enables the creation of a new Prebid Demand Partner Param object.

### Example call using cURL

```
curl -d @demand-partner-params.json -X POST --header "Content-Type: application/json" 'https://api.appnexus.com/prebid/prebid-demand-partner-params'
```

### Parameters

| Name | Type | Scope | Description |
|:---|:---|:---|:---|
| `name` | string | Required | The name of the Prebid demand partner. |
| `enabled` | boolean | Required | Indicates if the Prebid demand partner params are enabled or disabled. |
| `member_id` | integer | Required | The caller's member ID. |
| `params` | object | Required | An object containing the parameters supported by the partner and the mapped values. Supported parameters can be found [here](demand-partner-schema-service.md). |
| `prebid_settings_id` | integer | Required | The `prebid_settings` ID. |

### `POST`: Example response

```
[
   {
      "id":3333333,
      "prebid_settings_id":222222,
      "name":"appnexus",
      "member_id":11111,
      "params":{
         "placement_id":123456
      },
      "enabled":true,
      "deleted":false,
      "last_modified_by":"user@domain.com",
      "last_modified":"2023-05-01T18:23:09.045Z"
   }
]            
            
```

## `PUT`

Updates an existing Prebid demand partner param. Include the `prebidDemandPartnerParamId` as the last component of the URL path. Pass the update information as JSON in the body of the request.

### `PUT`: Example call using cURL

```
curl -d @config-update.json -X PUT --header "Content-Type: application/json https://api.appnexus.com/prebid/prebid-demand-partner-params/{prebidDemandPartnerParamId}
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
