---
title: Create a Custom Role using the API
description: In this article, learn step-by-step instructions on how to create a custom role using the API.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Create a custom role using the API

A role is a set of permissions that is assigned to a user. In addition to the platform roles such as **Network Admin**, you can also create custom roles, that have just the set of permissions you want.

The way the API grants user permissions is by granting a user access to *resources*.

This page shows you how to create a custom role using the API.

## Step 1: Determine the role resources

When designing a custom role, first you have to determine what resources the role will have access to. For example, a role could have access to resource ID 157, `"UI API Ad Profile Create"`, which will allow users in that role to create [ad profiles](ad-profile-service.md).

To see the list of resources in the system that a member's users could potentially have access to, see [View System Resources using the API](view-system-resources-using-the-api.md).

In this example, our custom role will have access to the following resources:

| ID | Role |
|:---|:---|
| 1 | API Yield Auction Tier Create |
| 2 | API Payment Rule Read |

## Step 2: Create role JSON

To give our new role access to these resources, we'll need to upload a JSON object like the one below.

> [!NOTE]
> The `name` and the list of `resources` are required.

Here's a "first draft" of the role JSON, which we'll need to add to in the next step.

```
{
   "access-member-role" : {
      "description" : "Auction Tiers and Payment Rules Only",
      "resources" : [
         {
            "id" : 1
         },
         {
            "id" : 2
         }
      ],
      "name" : "[test] auction-tier-payment-rule"
   }
}
```

## Step 3: Find out resource dependencies

A given resource often has dependencies on other, more general esources. To give your custom role access to all of the system resources it needs, you must specify and add all of the dependencies manually.

To make this easier, there is an API service you can use to find the dependencies you need. Make a `GET` call to the **Access Resource Dependency List Service** service as shown below. You must include the `resource_id` query string parameter.

```
$ curl -b /Users/username/.x-api-client/usor-env-cookies -X GET \
'https://api.appnexus.com/access-resource-dependency-list?resource_id=1'
```

You'll get back a list of resource IDs in the `children` field. You'll need to add these IDs to your role JSON.

> [!NOTE]
> These dependencies may have their own dependencies.

```
{
   "response" : {
      "access-resource-dependency-list" : [
         {
            "children" : [
               153,
               163,
               171
            ],
            "resource_id" : 1,
            "parents" : [
               146
            ],
            "dependencies" : [
               153,
               163,
               171
            ]
         }
      ],
      "count" : 1,
      "start_element" : 0,
      "status" : "OK",
      "num_elements" : 0
   }
}
```

> [!TIP]
> Getting more information about a resource
>
> If you want more information about any of a resource's dependencies, take a look at it using the instructions in [View System Resources using the API](view-system-resources-using-the-api.md).

## Step 4: Update role JSON with resource dependencies (if needed)

If your custom role's resources have any dependencies, add them to the role JSON. It should look like the sample below.

```
{
   "access-member-role" : {
      "name" : "[test] auction-tier-payment-rule",
      "resources" : [
         {
            "id" : 1
         },
         {
            "id" : 2
         },
         {
            "id" : 153
         },
         {
            "id" : 163
         },
         {
            "id" : 171
         }
      ],
      "description" : "Auction Tiers and Payment Rules Only"
   }
}
```

## Step 5: `POST` role JSON

`POST` the role JSON to the **Access Member Role Service**.

```
$ curl  -b cookies -X POST -d '@create-custom-role.json' \
'https://api.appnexus.com/access-member-role?member_id=1282'
```

If all goes according to plan, you'll see a response like the one below. If you forgot to specify a resource's complete list of dependencies, you'll get back an error with the resource IDs of the dependencies you need.

```
{
   "response" : {
      "access-member-role" : [
         {
            "id" : 113,
            "last_modified" : "2016-04-04 21:05:48",
            "resources" : [
               {
                  "name" : "hbapi-ym-auction-tier-post",
                  "id" : 1
               },
               {
                  "id" : 2,
                  "name" : "hbapi-payment-rule-get"
               },
               {
                  "id" : 153,
                  "name" : "hbapi-ym-auction-tier-get"
               },
               {
                  "id" : 163,
                  "name" : "hbapi-ym-profile-get"
               },
               {
                  "name" : "hbapi-publisher-get",
                  "id" : 171
               }
            ],
            "description" : "Auction Tiers and Payment Rules Only",
            "member_id" : 1282,
            "name" : "[test] auction-tier-payment-rule"
         }
      ],
      "start_element" : 0,
      "status" : "OK",
      "count" : 1,
      "num_elements" : 1
   }
}
```

## Related topics

- [Working with Roles using the API](working-with-roles-using-the-api.md)
- [Add a User to a Role using the API](add-a-user-to-a-role-using-the-api.md)
- [View System Resources using the API](view-system-resources-using-the-api.md)
