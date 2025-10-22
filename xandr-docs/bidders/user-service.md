---
title: Bidders - User Service
description: Explore managing API access for individuals or groups with the User Service. Categorize users as bidders or members.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - User service

Here "user" refers to people or groups using Xandr's APIs. The User Service will allow you to manage who has access to Xandr's APIs. Users are classified as by a user type of either *bidder* or *member*.

- Bidder users can be created by other bidder users.
- A bidder-user can create and update member-users as well as update its own user info.
- A member-user can update its own user info.
- Each new username associated with a particular bidder must be unique.

## REST API

| HTTP Method | Endpoint | Description |
|--|--|--|
| GET | `https://api.adnxs.com/user` | View all the users that you have created. |
| GET | `https://api.adnxs.com/user/USER_ID` | View a particular user. |
| POST | `https://api.adnxs.com/user` (user JSON) | Add a user. |
| PUT | `https://api.adnxs.com/user/USER_ID` (user JSON) | Modify an existing user. |

To delete an existing user:  
DELETE [https://api.adnxs.com/user/USER_ID](https://api.adnxs.com/user/USER_ID)

## JSON structure

| Field | Required | Type | Description |
|--|--|--|--|
| id | yes (on update) | int | Internal ID associated with the user. |
| active | no | Bool | Currently you cannot delete a user. For now, set to active to "false" |
| username | yes (on add) | string(50) | Name of the user. User names must be unique.<br><br>**Note**: After a user is created, the username cannot be changed. |
| password | yes (on add) | string | Password for the user. |
| email | yes | string | Email of the user. (Note that a user can be created without an email, but this will cause problems later when trying to update the user.) |
| user_type | yes | enum('bidder','member') | Type of user being added. |
| read_only | no | Boolean | Users with read_only field set to true can not add, modify, or delete resources. |
| entity_id | yes (on add) | int | ID of the entity the user belongs to (member or bidder). If the user_type is "bidder" this is the bidder ID. If the user_type is "member" this is the member ID. |
| entity_name | no | string | Name of the entity the user belongs to (member or bidder). |
| first_name | no | string | User's first name |
| last_name | no | string | User's last name |
| phone | no | string | User's phone contact |
| publisher_id | no | string | This field is only used for Displaywords |
| advertiser_id | no | string | This field is only used for Displaywords |
| advertiser_access | no | array of objects | The advertiser(s) that the user can access, if `user_type` is `"member_advertiser"`. |
| publisher_access | no | array of objects | The publisher(s) that the user can access, if `user_type` is `"member_publisher"`. |
| api_login | no | Boolean | True if the user has access to the API. Default is False.<br> This is an admin-only field. If you create a new user who needs API access, contact customer support to request that this value be set to True. |
| custom_data | no | string | Any information relevant to the user. |
| send_safety_budget_notifications | no | Boolean | If `true`, the user will receive email notifications when the daily safety budget threshold is approached. For more details, see the `daily_budget` field on the  [Member Service](member-service.md). |
| timezone | no | string | The user's timezone. |
| entity_reporting_decimal_type | no | string | Whether number values are separated by a comma or a decimal in reports. If this field is set to decimal, the value returned would be formatted like this: 1234.56. Whereas, if this field is set to `comma`, the value returned would be formatted like this: 1234.56.<br>Possible values:<br> - `decimal`<br> - `comma` |
| reporting_decimal_type | no | string | The character used for decimals in reporting. Possible values:<br> - `"comma"`<br> - `"decimal"` (period)<br>This setting can be overridden at the report level (see `reporting_decimal_type` in the  [Report Service](report-service.md)). |
| decimal_mark | no | string | The character used to represent a decimal mark, such as "period" for a value of 12.7. |
| thousand_seperator | no | string | The character used to separate thousands in numeric values, such as "comma" for the value 1,276. |
| last_modified | no | date | The date the any of the user settings were last modified. |
| is_developer | no | Boolean | **Read-only**. This flag gives a user rights to access certain developer-focused services such as the Plugin and Plugin Instance services, which are used by apps. It is set to true by a Xandr admin on a case-by-case basis. |
| role_id | no | int | The ID of the role associated with this user. |
| password_expires_on | no | date | The date the user password expires. |
| password_last_changed_on | no | date | The date the user's password was last changed. |

## Examples

**Authentication token**

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. Please see [Authentication Service](authentication-service.md) for more detailed instructions.

**Create a user profile text file**

To give API access to "TestUser," you will create a text file in JSON format with the username and password of the user, and the ID of either a member or bidder to which this user will belong. Below we have used the "cat" command to output an example user JSON file.

```
$ cat user
{
   "user":{
      "username":"TestUser",
      "password":"2323test",
      "entity_id":7,
          "email": "user1@examplecompany.com",
          "user_type": "bidder"
   }
}
```

**Guidelines for creating your password**

When creating your password, please create a complex password with the
following:

- 10 or more characters
- 64 or fewer characters
- At least one capital letter (A–Z)
- At least one lowercase letter (a–z)
- At least one digit (0–9)
- At least one special character (such as \#, $, ? %, &)

**Add a new user to the Imp Bus cache**

Now we will input the user file. We have used cookies to authenticate
ourselves.

```
$ curl -b cookies -c cookies -X POST --data-binary @user https://api.adnxs.com/user
{
   "response":{
      "status":"OK",
      "id":59
   }
}
```

**Retrieve user information from the Imp Bus cache**

We know from the output of the above command that the user we just added has been assigned ID \#59 by the Imp Bus. We can use that ID to view information about this particular user. To see all users that we have created, we would leave off the user ID.

```
$ curl -b cookies -c cookies https://api.adnxs.com/user/59
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "user": {
      "id": 59,
      "active": true,
      "first_name": null,
      "last_name": null,
      "phone": null,
      "username": "TestUser",
      "email": "user1@examplecompany.com",
      "user_type": "bidder",
      "read_only": false,
      "api_login": false,
      "entity_id": 7,
      "publisher_id": null,
      "advertiser_id": null,
      "custom_data": null,
      "send_safety_budget_notifications": false,
      "entity_name": "Platform Services Test Bidder",
      "timezone": null,
      "entity_reporting_decimal_type": null,
      "reporting_decimal_type": null,
      "decimal_mark": "period",
      "thousand_separator": "comma",
      "last_modified": "2017-02-16 19:06:47",
      "is_developer": false,
      "role_id": null,
      "languages": null,
      "advertiser_access": null,
      "publisher_access": null
    },
    "dbg": {
                ...
    }
  }
}
```

**Request API access**

Notice in the returned code above the **api_login** field. This field can only be changed by a Xandr administrator. The final step in giving a user access to the API is to contact customer support and request that the **api_login** flag for the user be set to **true**. Be sure to include username or ID in the request.

## Related topic

[API Services](api-services.md)
