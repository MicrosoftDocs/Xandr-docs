---
title: Native Custom Key Service
description: Use the Native Custom Key service to view and store custom key values for members' ads with a creative format ID of 12.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Native Custom Key service

The **read-only** Native Custom Key Service is used to view the custom keys that belong to a certain member. Native custom keys are used by native ad creatives. Technically, native ads are identified by our system as those creatives that have a `template` with a `creative_format_id` of `12`, i e., `"native"`. Some sellers allow buyers to send along custom values with native ads, such as the advertiser's brand, and native custom keys are used to store this information.

## JSON fields

| Name | Type | Sort by? | Filter by? | Description |
|:---|:---|:---|:---|:---|
| `id` | int | No | No | **Deprecated**<br><br>**Default**: N/A<br> |
| `custom_key` | string | No | Yes | **Deprecated**<br><br>**Default**: `null`<br> |
| `last_modified` | date | No | No | **Deprecated**<br><br>**Default**: Same as `created_on`, until modified.<br>**Required On**: N/A |
| `created_on` | date | No | No | **Deprecated**<br><br>**Default**: N/A<br>**Required On**: N/A |

## Example

### View all of the native custom keys associated with a member

View a member's native custom keys:

```
$ curl -b cookies 'https://api.appnexus.com/native-custom-key?member_id=123'
{
   "response":{
     "status":"OK",
     "count":1,
     "start_element":0,
     "num_elements":100,
     "native_custom_keys":[
       {
         "id":1,
         "custom_key":"object",
         "last_modified":"2015-03-10 22:34:39",
         "created_on":"2015-03-10 22:34:39" 
      }
    ]
  }
}
      
```

## Related topics

- [Member Service](./member-service.md)
- [Creative Service](./creative-service.md)
- [Media Subtype Service](./media-subtype-service.md)
