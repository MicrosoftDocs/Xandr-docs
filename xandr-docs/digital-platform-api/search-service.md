---
title: Search Service
description: Explore the Search service to search for objects without specifying an object type.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Search service

The universal search service makes it easier to search for objects without specifying an object type. We found that many clients use codes in the naming convention of objects that are associated to each other and you can us the universal search service in order to pull all objects associated with that code. You can also use universal search service to search for objects within a certain object type.

> [!NOTE]
> The Search Service is different from the [Lookup Service](lookup-service.md) because it allows you to search for objects with a specific name, code, or ID. The Lookup Service returns all objects of a certain type in your account.  
>
> You can also search and filter using individual services. For details, see [API Semantics](api-semantics.md).

## Using search with no parameters

If you would like to search for objects across all object types that have the term "hairspray" in them, you can do so by posting `'api.appnexus.com/search?q=hairspray'`. This will return objects that have hairspray in the name, ID, or code.

The API will automatically return results for the following object types:

- advertiser
- insertion order
- line items
- campaigns
- creatives
- segment pixels
- conversion pixels
- publishers
- placements
- sites

## Using search with a parameter

If you would like to use universal search to search for a certain object type, you can include a parameter: `"type=creative"`.

## Search results

When you do not specify a certain object type, we will return 30 objects per object type.

> [!NOTE]
> Xandr indexes the first 42 characters of each word. If an individual word is longer than 42 characters, and you search for characters after the 42nd, your search will not return the results you're looking for.

## Example

### Example code snippet

> [!NOTE]
> The `"weight"` parameter is a very rough estimation of search match, but is not reliable and should be ignored for now.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/search?type=advertiser&q=test'
{
    "response": {
        "status": "OK",
        "num_elements": 3,
        "start_element": 0,
        "results": {
            "advertiser": {
                "num_elements": 3,
                "results": [
                    {
                        "id": "40543",
                        "weight": "1539",
                        "name": "Test Advertiser 001",
                        "code": "",
                        "member_id": "1173",
                        "state": "active"
                    },
                    {
                        "id": "40737",
                        "weight": "1539",
                        "name": "Test Advertiser 002",
                        "code": "",
                        "member_id": "1173",
                        "state": "active"
                    },
                    {
                        "id": "41351",
                        "weight": "1539",
                        "name": "Contest Advertiser",
                        "code": "",
                        "member_id": "1173",
                        "state": "active"
                    }
                ]
            }
        }
    }
}
```
