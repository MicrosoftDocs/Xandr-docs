---
title: Campaign Object Service
description: Learn about the Campaign Object Service API for creating PSP configurations with targeting, demand mapping, and automation in Monetize.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Campaign Objects Service

The **Prebid Server Premium (PSP) UI** allows configuration creation, including targeting (geographic location, device, key value, etc.) and demand partner mapping, in a single workflow. See [Create a New PSP Configuration](../monetize/create-a-psp-configuration.md) for context and UI guidance.

Creating such configurations via **API** requires the PSP campaign objects service, detailed below, to set the desired targeting. The response from this service includes a `lineItem.id` which is then set as the `targeting_id` in the [configuration service](config-service.md).

The new PSP campaign objects service:

- Creates an **advertiser** (if a PSP advertiser does not exist).
- Creates an **insertion order** (if a PSP insertion order does not exist).
- For each call, creates a **new profile and line item pair**.

These are PSP-specific shell objects that do not deliver but are necessary for the targeting profile to be evaluated by the **Monetize Platform**. Only the profile portion is relevant to the publisher for any `POST`/`PUT`/`PATCH` calls to this PSP service.

It is recommended to manage these configurations and their targeting in the [PSP UI](../monetize/create-a-psp-configuration.md), but for large publishers or those with automation, **API interaction** is required or at least preferred.

## High-level workflow

1. Make a **POST** request to `https://api.appnexus.com/prebid/psp-campaign-objects` with the desired targeting.
1. Record the `lineItem.id` value.
1. Make a **POST**/**PUT**/**PATCH** request to `https://api.appnexus.com/prebid/config` where the `targeting_id` is the `lineItem.id` from the PSP campaign objects service response.

> [!NOTE]
> Do not delete any of the objects created by this service. Deleting the advertiser, insertion order, line items, or profiles associated with PSP configurations will break the configurations, prevent bid requests from being sent to demand partners, and prevent monetization of the affected inventory through PSP.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/prebid/psp-campaign-objects](https://api.appnexus.com/prebid/psp-campaign-objects) | Create PSP targeting and all prerequisite objects (advertiser, insertion order, line item, profile). |
| `PUT` | [https://api.appnexus.com/prebid/psp-campaign-objects?profileId={ProfileID}&lineItemId={LineItemID}}](https://api.appnexus.com/prebid/psp-campaign-objects?profileId={ProfileID}&lineItemId={LineItemID}}) | Overwrite PSP targeting. |

## `POST`

### POST: Parameters

| Property | Type| Description|
|---|---|---|
| advertiser| object | The automatically created advertiser to house all PSP objects. DO NOT DELETE this object or any associated configurations will break. See advertiser service documentation for more information.|
| insertionOrder| object| The automatically created advertiser to house all PSP line items. **Do not delete this object or any associated configurations will break**. See insertion order service documentation for more information.|
| lineItem | object| The automatically created line item to carry the targeting profile for evaluation. DO NOT DELETE this object or any associated configurations will break. See line item service documentation for more information.|
| profile | object| The profile created based on the input from the initial POST call. Determines which publisher bid requests will initiate the PSP configuration. See profile service documentation for structure and details.|

### POST Response

| Property| Type| Description |
|---|---|---|
| advertiser | object| The automatically created advertiser to house all PSP objects. DO NOT DELETE this object or any associated configurations will break. See advertiser service documentation for more information. |
| insertionOrder | object | The automatically created advertiser to house all PSP line items. DO NOT DELETE this object or any associated configurations will break. See insertion order service documentation for more information. |
| lineItem| object | The automatically created line item to carry the targeting profile for evaluation. DO NOT DELETE this object or any associated configurations will break. See line item service documentation for more information. |
| profile| object| The profile created based on the input from the initial POST call. Determines which publisher bid requests will initiate the PSP configuration. See profile service documentation for structure and details.|

### Creating objects

1. Make a **POST** request to [`https://api.appnexus.com/prebid/psp-campaign-objects`](https://api.appnexus.com/prebid/psp-campaign-objects)

    1. Include a top-level [profile object](profile-service.md):
    1. The profile object must include a `name` string.
    1. The profile object must contain any desired targeting as documented in the [profile service](profile-service.md).
    1. Note on the [profile service documenatation](profile-service.md) like certain fields, like `country_targets`, include a corresponding `_action` field, such as `country_action`. The `_action` field is set to **include** or **exclude**.  If set to **include**, the corresponding object/array (e.g., `country_targets`) must be populated for the targeting to function.
    1. Values to populate within the profile can be found in **read-only services**, such as the [country service](country-service.md). These are linked in the [profile service documentation](profile-service.md).

   ### Example profile request

   ```
    {
    "profile": {
        "name": "Test Profile",
        "country_action": "include",
        "country_targets": [
            {

                "id": 233,
                "name": "United States",
                "code": "US",
                "active": true
            },

            {
                "id": 41,
                "name": "Canada",
                "code": "CA",
                "active": true
            },

            {
                "id": 80,
                "name": "United Kingdom",
                "code": "UK",
                "active": true
            }
          ]
        }
      }
     
    ```

1. The **PSP campaign objects service** will respond with the details of the objects created:

     - **advertiser**: Created if one did not already exist for PSP.  
     - **insertionOrder**: Created if one did not already exist for PSP.  
     - **profile**: Contains all of the targeting.  
     - **lineItem**: Includes the `id` value, which will be used as the `targeting_id` in the [PSP Configuration Service](config-service.md).

1. Make a **POST**, **PUT**, or **PATCH** request to [https://api.appnexus.com/prebid/config](https://api.appnexus.com/prebid/config) (documentation).

   1. `targeting_level_code` must be **4** (line item).  
   1. `targeting_id` is the `lineItem.id` from the PSP campaign objects service response.  
   1. `targeting_metadata.priority` is an integer **1 through 20**.

        1. Each auction uses one configuration.  
        1. If the targeting of multiple configurations overlaps, the `targeting_metadata.priority` determines which configuration is chosen, with **20** being the highest priority.

   ### Example configuration request

   Append the configuration ID as the last component of the URL.

    ```

    {
    "name": "Test Configuration",
    "targeting_level_code": 4,
    "targeting_id": 26831593,
    "enabled": true,
    "media_types": {

        "types": [
            "banner",
            "video",
            "native"
        ]
    },

    "targeting_metadata": {
        "priority": 18
    },

    "demand_partner_config_params": [
        {
            "name": "appnexus",
            "params": {

                "placement_id": 123456
            }
          }
        ]
      }
   ```

1. The [configuration service](config-service.md) will respond confirming the details of the objects (configuration, and optionally demand partner configuration parameters) created.

## `PUT`

### Editing objects

1. Retrieve the details of the profile created earlier by the PSP campaign objects service. Refer to the [profile service documentation](profile-service.md):
     1. If the `advertiser.id` from the previous call to the PSP campaign objects service is not known is not known, refer to the [advertiser service documentation](advertiser-service.md). Make a **GET** request to `https://api.appnexus.com/advertiser`.
     1. Make a **GET** request to [https://api.appnexus.com/profile?advertiser_id=ADVERTISERID](https://api.appnexus.com/profile?advertiser_id=ADVERTISERID) to retrieve all profiles for the advertiser, or [https://api.appnexus.com/profile?code=PROFILEID&advertiser_code=ADVERTISERID](https://api.appnexus.com/profile?code=PROFILEID&advertiser_code=ADVERTISERID) to retrieve a specific profile.
     1. The Profile service will respond with the full profile object, containing all possible targeting fields.  Although `PATCH` requests to PSP campaign objects are not yet supported, the **PUT** request only needs to include the profile targeting elements to be updated.
     1. If the `lineItem.id` is not known, refer to the **[line item service documentation](line-item-service---ali.md). Make a **GET** request to `https://api.appnexus.com/line-item`.

1. Make a **PUT** request to [https://api.appnexus.com/prebid/psp-campaign-objects?profileId=PROFILEID&lineItemId=LINEITEMID](https://api.appnexus.com/prebid/psp-campaign-objects?profileId=PROFILEID&lineItemId=LINEITEMID)
     1. Include a top-level [profile object](profile-service.md).
     1. The profile object must contain any desire.

   ### Example call using curl

   ```
   {

   "profile": {
   "country_action": "include",
   "country_targets": [
   {
   "id": 233,
   "name": "United States",
   "code": "US",
   "active": true
   },

   {
   "id": 41,
   "name": "Canada",
   "code": "CA",
   "active": true
   },

   {
   "id": 80,
   "name": "United Kingdom",
   "code": "UK",
   "active": true
    },
    {
    "id": 34,
    "name": "Brazil",
    "code": "BR",
    "active": true
  
         }
        ]
       }
      }

    ```

1. The PSP campaign objects service will respond with the details of the objects updated.

## Related topics

- [Configuration Service](config-service.mdvice)
- [Cross-Partner Settings Service](cross-partner-settings-service.md)
- [Demand Partner Service](demand-partner-service.md)
- [Demand Partner Schema Service](demand-partner-schema-service.md)
- [Prebid Demand Partner Params Service](prebid-demand-partner-params-service.md)
- [Create a New PSP Configuration](../monetize/create-a-psp-configuration.md)
- [Prebid Server Premium Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md)
- [Common Issues and Best Practices](../monetize/psp-common-issues-and-best-practices.md)