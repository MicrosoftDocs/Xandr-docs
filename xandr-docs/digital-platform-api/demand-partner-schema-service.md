---
title: Demand Partner Schema Service
description: Use the Demand Partner Schema service to validate which parameters are accepted by the demand partner.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Demand Partner Schema service

The Demand Partner Schema Service validates which parameters are accepted by the demand partner. The service returns all demand partner schemas for the caller's member.

Demand Partner Schemas are unique per demand partner, as each demand partner will have a different set of parameters required at auction time when a particular PSP configuration is processed. There is no way to fetch a schema for a specific demand partner. We only allow a way to see all schemas for valid PSP demand partners.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/prebid/demand-partner-schemas` | Return all demand partner schemas. |

### Example response

```
{
   "33across":{
      "$schema":"https://json-schema.org/draft-04/schema#",
      "description":"A schema which validates params accepted by the 33Across adapter",
      "properties":{
         "productId":{
            "description":"Product type",
            "type":"string"
         },
         "siteId":{
            "description":"Site Id",
            "type":"string"
         },
         "zoneId":{
            "description":"Zone Id",
            "type":"string"
         }
      },
      "required":[
         "productId",
         "siteId"
      ],
      "title":"33Across Adapter Params",
      "type":"object"
   },
   "adform":{
      "$schema":"https://json-schema.org/draft-04/schema#",
      "description":"A schema which validates params accepted by the Adform adapter",
      "properties":{
         "mid":{
            "description":"An ID which identifies the placement selling the impression",
            "type":[
               "integer",
               "string"
            ]
         },
         "mkv":{
         "description":"Comma-separated key-value pairs. Forbidden symbols: &. Example: mkv='color:blue,length:350'",
         "pattern":"^(\\s*|(([^,:&]*[^,:&\\s]+[^,:&]*)+:[^,:&]*,)*(([^,:&]*[^,:&\\s]+[^,:&]*)+:[^,:&]*,?))$",
            "type":"string"
         },
         "mkw":{
         "description":"Comma-separated keywords. Forbidden symbols: &.",
         "pattern":"^[^&]*$",
            "type":"string"
         },
         "priceType":{
            "description":"An expected price type (net or gross) of bids.",
            "enum":[
               "gross",
               "net"
            ],
            "type":"string"
         }
      },
      "required":[
         "mid"
      ],
      "title":"Adform Adapter Params",
      "type":"object"
   }
}
```

## Related topics

- [Prebid Demand Partner Params Service](./prebid-demand-partner-params-service.md)
- [PSP Demand Partner Integrations](../monetize/prebid-server-premium-demand-partner-integrations.md)
- [Add or Edit a Demand Partner](../monetize/add-or-edit-a-demand-partner.md)
- [Add, Edit, or Delete a PSP Configuration](../monetize/add-edit-or-delete-a-psp-configuration.md)
