---
title: Brand Company Service
description: In this article, find information about the Brand Company Service and the fields associated with it.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Brand company service

Each brand is associated with a company, which can be used for filtering and searching. You can use the read-only Brand Company Service to list these companies. Brand companies are used primarily in developing [Ad Profiles](ad-profile-service.md) that determine what brands are allowed to run on certain publishers' pages.

For more information about brands, see [Brand Service](brand-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | `https://api.appnexus.com/brand-company` | To view all the brand categories |
| `GET` | `https://api.appnexus.com/brand-company?id=BRAND_COMPANY_ID` | To view information about a particular brand category |

## JSON fields

| Field | Type | Description |
|---|---|---|
| `id` | int | The ID of the brand. |
| `last_modified` | string | A timestamp of when the record was last modified. |
| `name` | string | Brand company name. |

## Example

### View all brand companies (below output is truncated)

```
curl -b cookies -c cookies "https://api.appnexus.com/brand-company"
{
    "response": {
        "brand-companies": [
            {
                "id":1,
                "name":"Amazon",
                "last_modified":"2010-06-20 15:45:00"
            },
            ...
        ],
        "status": "OK"
    }
}
```

## Related topics

- [Category Service](category-service.md)
- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
