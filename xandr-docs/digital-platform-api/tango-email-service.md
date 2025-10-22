---
title: Tango Email Service
description: Use the Tango Email and Email Template services to manage system emails for Tango without relying on API team for quick iteration and deployment of changes.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Tango Email service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This service, used in combination with the [Email Template Service](./email-template-service.md), enables team to manage the sending of system emails for Tango. Allowing  team to manage system emails rather than the API team provides the Tango team the ability to more quickly iterate and deploy system email changes.

> [!NOTE]
> While this service is visible to all members, it should only be used by Xandr employees. Therefore, this documentation will only be visible to Xandr employees until further notice.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/tango-email`<br>(`send_email` JSON) | Send a system email. |

## JSON fields

| Name | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the email message that is sent.<br><br>**Default**: Auto-incremented number. |
| `email_id` | int | The ID of the template that was used to populate and format the email. You can use the [Email Template Service](./email-template-service.md) to see the list of available email templates and their IDs.<br><br>**Required On**: `POST` |
| `sender_user_id` | int | **Read Only**. The ID of the user that sent the email (POSTed to this service). Administrators can set the value for this field to define an email sender other than themselves. |
| `sender_member_id` | int | **Read Only**. The ID of the member that is associated with the user that sent the email (POSTed to this service) . Administrators can set the value for this field to define an email sender other than themselves. |
| `recipient_user_id` | int | The ID of the user that should receive the email.<br><br>**Required On**: `POST` |
| `recipient_member_id` | int | The ID of the member that is associated with the user that should receive the email. |
| `partner_relationship_id` | int | The ID of the partner relationship that the email message is associated with.<br><br>**Required On**: `POST` |
| `partner_relationship_deal_id` | int | The ID of the trade that the email message is associated with. |
| `additional_fields` | array of objects | You can use this array to define a value for any additional macros that may exist in the email template you have defined in the `email_id` field. For example, if your email template includes a `%deal_name%` data placeholder you can include `deal_name = "My Favorite Deal"` in this array to provide the deal name that should display within the email text. |
| `recipient_is_buyer` | boolean | If `true`, the recipient of the email is the buyer in the partner relationship. This field is not currently being used.<br><br>**Default**: `false` |

## Examples

### Send a system email

```
$ cat send_email
{
 "tango_email":
  {     "email_id" : 19,
        "recipient_member_id" : 3837,
        "partner_relationship_id" : 175
  }
}
```

```
$ curl -b cookies -c cookies -X POST -d @send_email.json "https://api.appnexus.com/tango-email"
{
  "response": {
    "status": "OK",
    "id": 0,
    "count": 1
  }
}
```
