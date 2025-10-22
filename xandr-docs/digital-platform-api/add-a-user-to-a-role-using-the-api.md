---
title: Add a User to a Role using the API
description: This article provides instructions for adding a user to a role using the API.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Add a user to a role using the API

This page has instructions for adding a user to a role.

For general information about roles, see [Working with Roles using the API](./working-with-roles-using-the-api.md).

For instructions on creating your own roles, see [Create a Custom Role using the API](./create-a-custom-role-using-the-api.md).

## Step 1. Create user role JSON

In this example we'll add a user to the role with role ID `35`. Here's the JSON we need. Note that the `user_id` and `role_id` are required:

```
$ cat add-user-role.json
{
   "access-member-user-role" : [
      {
         "user_id" : 1234,
         "role_id" : 35
      }
   ]
}
```

## Step 2. `POST` user role JSON to the user role API

Now `POST` the user role JSON to the **Access Member User Role Service** to make the update:

```
$ curl -b cookies -X POST -d '@add-user-role.json' "https://api.appnexus.com/access-member-user-role?user_id=1234&member_id=1282" 
{
   "response" : {
      "count" : 1,
      "num_elements" : 1,
      "status" : "OK",
      "access-member-user-role" : [
         {
            "user_id" : 1234,
            "id" : 142,
            "role_id" : 35,
            "platform_role" : false
         }
      ],
      "start_element" : 0
   }
}
      
```

Now we can take a look at the user's assigned role. Because this is a custom role, `"platform_role"` is `false`.

```
{
   "response" : {
      "status" : "OK",
      "access-member-user-role" : [
         {
            "user_id" : 1234,
            "role_id" : 35,
            "platform_role" : false,
            "id" : 142
         }
      ],
      "count" : 1,
      "num_elements" : 1,
      "start_element" : 0
   }
}
      
```
  
You can also assign multiple roles to a single user:

```
$ cat add-multiple-user-roles.json
{
   "access-member-user-role" : [
      {
         "user_id" : 1234,
         "role_id" : 35
      },
      {
         "user_id" : 1234,
         "role_id" : 12
      },
      {
         "user_id" : 1234,
         "role_id" : 41
      }
   ]
}
```

## Related topics

- [Working with Roles using the API](./working-with-roles-using-the-api.md)
- [Create a Custom Role using the API](./create-a-custom-role-using-the-api.md)
- [View System Resources using the API](./view-system-resources-using-the-api.md)
