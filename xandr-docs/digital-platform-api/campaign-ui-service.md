---
title: Campaign UI Service
description: In this article, learn about the Campaign UI service, their JSON fields, and REST API with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Campaign UI service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

The Campaign UI service includes campaign meta information relating to campaign peer approval settings, including campaign creator and approver information. You can use it to determine whether peer approval is required for campaigns created by a specific user.

> [!NOTE]
>
> - Campaign UI settings are not enforced in the service layer for campaign activation. This API service does not interact with API logic. The service cannot actually change campaign settings and cannot prevent unapproved campaign creation by a user in the API. Rather, the Campaign UI service's purpose is exclusively to maintain the permissions for GUI use cases around campaign activation, and to assist with workflow management in.
> - This service is accessible only to the following user types:
>   - `member`
>   - `advertiser`
>   - `member_advertiser`

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/campaign-ui](https://api.appnexus.com/campaign-ui)<br>(Campaign UI JSON)  | Create a new campaign UI object. |
| `PUT` | [https://api.appnexus.com/campaign-ui?id=ID](https://api.appnexus.com/campaign-ui?id=ID) | Modify user data contained in a campaign UI object. |
| `GET` | [https://api.appnexus.com/campaign-ui](https://api.appnexus.com/campaign-ui) | View all campaign UI settings. |
| `GET` | [https://api.appnexus.com/campaign-ui?id=ID](https://api.appnexus.com/campaign-ui?id=ID) | View campaign UI settings for a specific campaign. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the corresponding campaign. Duplicate entries of the same campaign is not allowed.<br>**Required On:** `PUT`/`DELETE`, in query string. |
| `member_id` | int | **Read Only.** The ID of the member this campaign belongs to. |
| `user_id_creator` | int | The ID of the user who creates the campaign. |
| `username_creator` | string (50) | **Read Only.** The user name of the user who creates the campaign. |
| `first_name_creator` | string (50) | **Read Only.** The first name of the user who creates the campaign. |
| `last_name_creator` | string (50) | **Read Only.** The last name of the user who creates the campaign. |
| `user_id_approver` | int | The ID of the user who approves the campaign. This user and the target campaign must belong the same member. |
| `username_approver` | string (50) | **Read Only.** The user name of the user who approves the campaign. |
| `first_name_approver` | string (50) | **Read Only.** The first name of the user who approves the campaign. |
| `last_name_approver` | string (50) | **Read Only.** The last name of the user who approves the campaign. |

## Examples

### Create a campaign UI object associated with a specific campaign and user

```
$ cat campaign-ui.json
{
"campaign-ui": {
"id": "393404",
"user_id_creator": "6698"
}
}
$ curl -b cookies -c cookies -X POST -d @campaign-ui.json 'https://api.appnexus.com/campaign-ui'
{
"response" : {
"count" : 1,
"campaign-ui" : {
"username_creator" : "lhuangTestUser2",
"user_id_approver" : null,
"first_name_approver" : null,
"first_name_creator" : "Ling",
"user_id_creator" : 6698,
"username_approver" : null,
"last_name_creator" : "Huang",
"last_name_approver" : null,
"member_id" : 3897,
"id" : 393404
},
"status" : "OK"
}
}
```

### Modify campaign UI information

```
$ cat campaign-ui.json
{
"campaign-ui": {
"user_id_approver": "5771"
}
}
```

```
$ curl -b cookies -c cookies -X PUT -d @campaign-ui.json 'https://api.appnexus.com/campaign-ui?id=393404'
{
"response" : {
"count" : 1,
"campaign-ui" : {
"username_creator" : "lhuangTestUser2",
"user_id_approver" : 5771,
"first_name_approver" : "Lingshi",
"first_name_creator" : "Ling",
"user_id_creator" : 6698,
"username_approver" : "lhuang_test_member",
"last_name_creator" : "Huang",
"last_name_approver" : "Huang",
"id" : 393404
},
"status" : "OK"
}
}
```

### View campaign UI information for a specific campaign

```
$ curl -b cookies -c cookies -X GET 'https://api.appnexus.com/campaign-ui?id=393404'
{
"response" : {
"count" : 1,
"campaign-ui" : {
"username_creator" : "lhuangTestUser2",
"user_id_approver" : 5771,
"first_name_approver" : "Lingshi",
"first_name_creator" : "Ling",
"user_id_creator" : 6698,
"username_approver" : "lhuang_test_member",
"last_name_creator" : "Huang",
"last_name_approver" : "Huang",
"member_id" : 3897,
"id" : 393404
},
"status" : "OK"
}
}
```

### Delete a campaign UI object

```
$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/campaign-ui?id=393404'
{
"response" : {
"status" : "OK"
}
}
```
