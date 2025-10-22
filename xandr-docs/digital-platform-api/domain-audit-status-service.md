---
title: Domain Audit Status Service
description: Use the Domain Audit Status service to check whether specific domains are on the platform and how Xandr has classified them.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Domain Audit Status service

The Domain Audit Status Service lets you check whether or not specific domains are on the Xandr platform and, if they are, how Xandr has classified them. This service is particularly useful for sellers who are interested in migrating domains onto the platform but first want to make sure that the domains have not already been rejected by Xandr. Also, since audited domains generally see more fill, sellers can use this service to identify domains already on the platform that they would like Xandr to audit.

Here's how it works:

1. You `POST` a JSON file containing the domains that you are interested in. The JSON must be formatted as follows:

    ```
    {"urls": ["URL1.com","URL2.com","URL3.de"]}
    ```

   > [!NOTE]
   >  Xandr does not store the "https://" or "www." prefix for domains. Since this service will look for domains **exactly** as they ar written in your JSON, it is therefore best not to include these prefixes in the domains you want to check.

1. The response shows whether or not each domain is on the Xandr platform and, if it is, how Xandr has audited it. For the full list of details provided about each domain in the response, see [JSON Fields](#json-fields) below.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/url-audit-search` | View the audit status of one or more domains<br><br>**Note**: This is a read-only service. Although you `POST` a JSON file, no objects are created in the system. |

## JSON fields

For domains on the Xandr platform, all of the following fields will be shown in the response. For domains not on the Xandr platform, only the `url` and `found` (with a value of `false`) fields will be shown in the response.

| Field | Type | Description |
|:---|:---|:---|
| `audit_datetime` | timestamp | The date and time when the domain was audited by Xandr. |
| `audit_status` | enum | The audit status of the domain. Possible values: <br> - `audited` - The domain has passed the Xandr audit.<br> - `rejected` - The domain app has failed the Xandr audit (due to Xandr policy violations).<br> - `unaudited` - The domain was not audited.<br> - `unauditable` - The domain was not auditable.<br> - `pending` - Xandr audit is still pending for the domain (default value).<br> - `is_adserver` - The domain was not audited and was detected as an ad server domain. |
| `content_category_id` | int | The content category of the domain, as determined by Xandr. If `audit_status` is `"rejected"`, this will be `null`. You can use the read-only [Content Category Service](./content-category-service.md) to view more details about specific content categories. |
| `found` | boolean | If `true`, the domain is on the Xandr platform. |
| `id` | int | The Xandr ID for the domain. |
| `intended_audience` | enum | The intended audience of the domain, as determined by Xandr. Possible values: <br> - `"mature"` <br> - `"young_adult"` <br> - `"children"` <br> - `"general"`.<br>If `audit_status` is `"rejected"`, this will be `null`. |
| `reason` | string | If `audit_status` is `"rejected"` or `"unauditable"`, the reason provided by Xandr. Any other status this field will be blank. |
| `url` | string | The domain. |

## Examples

### View information about two domains on the platform

```
$ cat urls
{
    "urls": ["goodurl.com","badurl.com"]
}
$ curl -b cookies -c cookies -X POST -d @urls 'https://api.appnexus.com/url-audit-search'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "urls": [
            {
                "id": 3456,
                "url": "goodurl.com",
                "reason": null,
                "content_category_id": 8380,
                "intended_audience": "general",
                "audit_status": "audited",
                "audit_datetime": null,
                "found": true
            },
            {
                "id": 2194,
                "url": "badurl.com",
                "reason": "Landing page contains an excessive number or density of units",
                "content_category_id": null,
                "intended_audience": null,
                "audit_status": "rejected",
                "audit_datetime": null,
                "found": true
            }
        ]
    }
}
```

### View information about two domains that are not on the platform

```
$ cat urls
{
    "urls": ["not-there1.com","not-there2.com"]
}
$ curl -b cookies -c cookies -X POST -d @urls 'https://api.appnexus.com/url-audit-search'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": null,
        "num_elements": null,
        "urls": [
            {
                "url": "not-there1.com",
                "found": false
            },
            {
                "url": "not-there2.com",
                "found": false
            }
        ]
    }
}
```

### Determine which domains in a list have been audited

In this example, we search for two domains (`auditedurl.com` and `notauditedurl.com`). Both domains are on the platform, but information is returned only for the one that meets the query string criteria (`audit_status=audited`). The domain that does not meet the query criteria is still returned in the results, but with a `found` value of `false` because it wasn't found with the given query.

```
$ cat urls
{
    "urls": ["auditedurl.com","notauditedurl.com"]
}
$ curl -b cookies -c cookies -X POST -d @urls 'https://api.appnexus.com/url-audit-search?audit_status=audited'
{
    "response": {
        "status": "OK",
        "count": 2,
        "start_element": 0,
        "num_elements": 100,
        "urls": [
            {
                "id": 3456,
                "url": "auditedurl.com",
                "reason": null,
                "content_category_id": 8380,
                "intended_audience": "general",
                "audit_status": "audited",
                "audit_datetime": null,
                "found": true
            },
            {
                "id": 7890,
                "found": false
            }
        ]
    }
}
```
