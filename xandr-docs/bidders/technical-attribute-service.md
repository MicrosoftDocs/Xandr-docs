---
title: Bidders - Technical Attribute Service
description: Learn about Technical Attribute Service to see what technical attributes are registered in the Xandr system. This page also provides a code example to View all technical attributes.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Bidders - Technical attribute service

Use the read-only Technical Attribute Service to see what technical attributes are registered in the Xandr system and can apply to creatives. Technical attributes describe features of the creative such as whether it is an image, flash, video, is expandable, etc. Creatives are tagged with technical attributes, and ad profiles can be configured to include / exclude particular technical attributes.

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| DELETE | [https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID](https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID) | To delete a technical attribute (admin only) |
| GET | [https://api.adnxs.com/technical-attribute](https://api.adnxs.com/technical-attribute) | To view all technical attributes |
| GET | [https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID](https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID) | To view information about a particular technical attribute |
| POST | [https://api.adnxs.com/technical-attribute](https://api.adnxs.com/technical-attribute) | To add a technical attribute (admin only) |
| PUT | [https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID](https://api.adnxs.com/technical-attribute?id=TECHNICAL_ATTRIBUTE_ID) | To modify a technical attribute (admin only) |

## JSON fields

| Parameter | Type | Description |
|--|--|--|
| `id` | int | The ID of the technical attribute |
| `last_activity` | string | When the technical attribute was last modified. |
| `name` | string | Technical attribute name. |

## Example

**View all technical attributes**

``` 
curl -b cookies -c cookies "https://api.adnxs.com/technical-attribute"
{
   "response":{
      "status":"OK",
      "technical_attributes":[
         {
            "id":1,
            "name":"Image",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":2,
            "name":"Flash",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":3,
            "name":"Text",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":4,
            "name":"Video",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":5,
            "name":"DHTML",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":6,
            "name":"Expandable",
            "last_activity":"2010-05-19 21:43:24"
         },
         {
            "id":7,
            "name":"Audio",
            "last_activity":"2010-05-19 21:43:25"
         }
      ],
      "count":7,
      "start_element":null,
      "num_elements":null
   }
}
```

## Related topics

- [API Services](api-services.md)
- [Creative API Services](creative-api-services.md)
