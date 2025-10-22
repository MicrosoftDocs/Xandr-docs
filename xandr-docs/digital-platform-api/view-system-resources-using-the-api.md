---
title: View System Resources using the API
description: Learn how to view the system resources that you may assign to a role.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# View system resources using the API

The way the API grants user permissions is by granting access to *resources*. A resource describes a set of capabilities for a user. For example, resource ID 157 is `"UI API Ad Profile Create"`, which allows the user with access to that resource to create an ad profile using the API.

This page describes how to view the system resources that you may assign to a role. This is usually because you want to [Create a Custom Role using the API](create-a-custom-role-using-the-api.md).

To see what system resources a member can assign to user roles, make a `GET` call to the service. Be sure to include the `member_id` in the query string.

```
curl -bc 'https://api.appnexus.com/access-resource?member_id=1282'
```

The output is an array of system resource objects. Examine it to see what system resources the member has access to and could assign to a role. Each resource looks like this:

```
{
        "id": 157,
        "name": "hbapi-ad-profile-post",
        "description": "UI API Ad Profile Create",
        "system": "hbapi",
        "service": "/ad-profile",
        "action": "POST",
        "field": "",
        "resource_type": "api",
        "last_modified": "2016-03-28 18:00:08",
        "display_eligible": false
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](create-a-custom-role-using-the-api.md)
- [Add a User to a Role using the API](add-a-user-to-a-role-using-the-api.md)
