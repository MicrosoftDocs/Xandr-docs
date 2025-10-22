---
title: Access Policy Resource Service
description: In this article, learn about the Access Policy Resource service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Access Policy Resource service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The **access-policy-resource** service allows you to retrieve the resources based on resource type: UI or API.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/access-policy-resource](https://api.appnexus.com/access-policy-resource) | View all resources. |
| `GET` | [https://api.appnexus.com/access-policy-resource?resource_type=RESOURCE_TYPE](https://api.appnexus.com/access-policy-resource?resource_type=RESOURCE_TYPE) | View all resources for a given type. |

## JSON fields

### General

| Field | Type (Length) | Description |
|:---|:---|:---|
| `resources` | object | The ID and name of each resource in this role. |
| `resource_type` | string | The type of each resource within the associated resources object. Value will be either UI or API. |

### Resources

Full resource values can be retrieved by calling the access-resource service. For more information on retrieving resources, see [View System Resources using the API](view-system-resources-using-the-api.md).

| Field | Type (Length) | Description |
|:---|:---|:---|
| `token` | string | A string containing the resource. This string is a tokenized version of the name property returned by the access-resource service. For example here are the names and tokens for the resource *Delete an Ad Quality Rule using the API*:<br>access-resource name: hbapi-ad-quality-rule-delete<br>access-policy-resource token: hbapi:/ad-quality-rule: DELETE |

## Examples

### View all resources

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-resource'
{
    "access-policy-resource": [
        {
            "resource_type": "api",
            "resources": [
                {
                    "token": "hbapi:/ym-bias:POST"
                },
                {
                    "token": "hbapi:/ad-quality-rule:DELETE"
                },
                {
                    "token": "hbapi:/access-resource:GET"
                },
                        ...
}
```

### View all resources for a given type

```
$ curl -b cookies 'https://api.appnexus.com/access-policy-resource?resource_type=ui'
 
{
    "access-policy-resource": [
        {
            "resource_type": "ui",
            "resources": [
                {
                    "token": "ui:/ad-quality:GET"
                },
                {
                    "token": "ui:/buyside/advertiser/show:GET"
                },
                {
                    "token": "ui:/bias-rule:MANAGE"
                },
                ...
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
