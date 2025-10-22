---
title: Profile Summary Service
description: Explore the read-only Profile Summary service that retrieves the campaign IDs associated with the line item and profiles targeting the specified target types.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Profile Summary service

The Profile Summary service is a **read-only** service. Given a line item ID and a list of profile target types, this service returns the IDs of campaigns under the line item with profiles targeting the given target types. Currently, this service only supports line items with no more than 250 campaigns.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/profile-summary?entity_type=line_item&entity_id=12345&summary_fields=postal_code,city,region](https://api.appnexus.com/profile-summary?entity_type=line_item&entity_id=12345&summary_fields=postal_code,city,region) | For a specific line item, view the IDs of campaigns that are targeting specific target types.<br><br>**Note:**<br>In the example above, the `entity_id` is the ID of the line item for which you want to view this summary and `summary_fields` is the types of targeting that you want to include in the summary. Possible values for `summary_fields`: `postal code`, `city`, `region`, `dma`, `country`, `domain`, `domain_list`, `segment`, `age`, `gender`, `daypart`. You can combine up to 10 of these values in a comma-separated list.  |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `postal_code_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have postal code targeting. |
| `city_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have city targeting. |
| `region_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have region targeting. |
| `dma_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have designated market area targeting. |
| `country_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have country targeting. |
| `domain_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have domain targeting. |
| `domain_list_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have domain list targeting. |
| `segment_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have segment targeting. |
| `age_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have age targeting. |
| `daypart_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have daypart targeting. |
| `operating_system_family_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have operating system family targeting. |
| `operating_system_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have operating system targeting. |
| `browser_targeting_exists` | object | An object containing an array of the campaign IDs for any campaigns that have browser targeting. |
| `device_model_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have device model targeting. |
| `carrier_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have carrier targeting. |
| `device_type_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have device type targeting. |
| `supply_type_targets_exist` | object | An object containing an array of the campaign IDs for any campaigns that have supply type targeting. |

## Example

### View a targeting summary for campaigns with postal code, city, region, dma, or country targeting

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/profile-summary? entity_type=line_item&entity_id=12345&summary_fields=postalcode,city,region,dma,country'
{
   "response" : {
      "status" : "OK",
      "profile-summary" : {
         "city_targets_exist" : {
            "campaign_ids" : [
               248525
            ]
         },
         "dma_targets_exist" : {
            "campaign_ids" : [
               307780
            ]
         },
         "region_targets_exist" : {
            "campaign_ids" : [
               157094
            ]
         },
         "postal_code_targets_exist" : {
            "campaign_ids" : [
               294607,
               294833,
               295299,
               296262,
               296312,
               296313,
               296373,
               296374,
               296375,
               296376,
               296379,
               296670,
               296673,
               297266,
               300517
            ]
         },
         "country_targets_exist" : {
            "campaign_ids" : [
               244064,
               247283,
               247916,
               295936,
               295975,
               299938,
               299939,
               299940,
               299941,
               299942,
               300006
            ]
         }
      }
   }
}
```
